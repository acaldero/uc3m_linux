


# Introducción a Unix/Linux

## 1.- Comenzando
    
### A.-Entrar y Salir de la Cuenta

|  DOS   |  UNIX     |  VMS         | CMS/CP       |
|--------|-----------|--------------|--------------|
|  .     |  login    |  .           | logon        |
|  .     |  passwd   | set passwd   | password     |
|  .     | exit      | logout       | logoff       |


* login
    * Comandos que nos permiten entrar en nuestra cuenta
*  passwd
    * Permite cambiar la contraseña de entrada
    * El programa te pedira tu antigua password (comprueba que eres tu) y tambien te pedira la nueva 2 veces. Si te confundes, presiona la tecla control y la letra 'c' a la vez, y vuelve a ejecutar.
```bash
    [passwd]
    >          Batman:a999999# passwd
    >          Changing password for a999999
    >          Enter old password:
    >          Enter new password:
    >          Re-type new password:
    >          Password changed.
   ```

* exit
   * logout
   * Permite salir de la cuenta.
   * Usando el comando 'exit', puede indicarte que no saldras de la cuenta por que queda tareas tareas pendientes.
      Pon otra vez 'exit' y saldras. (En la mayoria de los Unix)
   * Tambien se sale con Control-D, solo en algunos shells.



### B.-Informacion de Recursos disponibles

|  DOS   |  UNIX     |  VMS         | CMS/CP       |
|--------|-----------|--------------|--------------|
|  .     | quota -v  |  sh quota    | q limits     |
| chkdsk |  df       |  .           | q v stor     |
|  .     |  du       |  .           | .            |
|  .     |  .        |  .           | q disk       |
|  .     |  .        |  .           | q time       |


* quota -v                        
    * Lista la cantidad de recurso asignado a ti y la cantidad ocupado (tiempo, Disco, ...)
    * A partir de los 1000 no te deja meter nada, y tendras el tiempo indicado por timeleft para quitar los (limit-quota) que sobran

```bash
[quota]
>          Batman:a999999# quota -v
>	   Disk quotas for a999999 (uid 999):
>	   Filesystem usage quota limit timeleft  files quota limit timeleft
>	   /u           683   950  1000              80    95   100
```

* df
    * Lista el espacio total+libre de cada una de las unidades.
* du
    * Lista el espacio que ocupa los fichero en el directorio actual y subdirectorios de este.


### C.-Optener Ayuda

|  DOS   |  UNIX     |  VMS         | CMS/CP       |
|--------|-----------|--------------|--------------|
| help   | man       |  help        | help         |

* <comando> --h
    * Cada vez se usa mas un nuevo estandar, reservar '--h'  para la ayuda.
* man <comando>
    * Presenta informa sobre el comando que se le indique (sintaxis, para que sirve y un monton de cosas mas).
    * Permite la opcion de usar parametros y manejar comandos internos:
      - Al llamarlo...:
        * man list          ---> Lista los comandos de unix por orden alfabetico de los que man tiene ayuda.
        * man -a <cmd> ---> Presenta toda la informacion que tenga el mismo nombre que <cmd>.
                                          Conforme se sale de la primera ayuda, se entra en la siguiente relacionada.
        * man -k <cmd> ---> Lista toda los comandos relacionados con <cmd> pero no presenta la ayuda de cada uno,
                                          como si lo hace la opcion -a.
      - Dentro de man... :
        * 'h'     ---> Lista de todas las funciones que hay dentro de man.
        * 'q'     ---> Sale del man.
        * ' '      ---> Siguiente pantalla.


## 2.- Ejecucion de comandos
    

### A.-Gestion de Procesos

|  DOS   |  UNIX     |  VMS                | CMS/CP       |
|--------|-----------|---------------------|--------------|
| <prog> | <prog>    | <prog> / run <prog> | <prog>       |
| .      | ps        | show system         | q names      |
| .      | kill -9   | STOP/IDENTIFICATION |.             |
| .      | Ctrl-z    | Ctrl-c              | .            |
| .      | jobs      | show sytem          | .            |
| .      | bg        | .                   | .            |
| .      | fg / %id  | continue            | attach       |
| .      | &         | spawn               | .            |
| .      | nohup     | submit              | disconnect   |
| .      | at        | submit/after        | cmsbatch     |


### B.-Interpretes de comandos : 'shells'

#### B.1.-'Shells' mas sencillos

|  DOS         |  UNIX                            |  VMS     | CMS/CP             |
|--------------|----------------------------------|----------|--------------------|
| dosshell     | .                                | swing    | filelist / dirlist |
| command.com  | bash,csh,ksh,sh,tcsh,zsh,mc,...  | .        | .                  |
    

#### B.2.-Como personalizar el 'shell'

|  DOS   |  UNIX     |  VMS       | CMS/CP   |
|--------|-----------|------------|----------|
| .      | chsh      | .          | .        |
    

##### B.2.1-VARIABLES DE ENTORNO

|  DOS         |  UNIX                        | VMS | CMS/CP |
|--------------|------------------------------|-----|--------|
| set ...=...  | set ...=... / setenv ... ... | .   | .      |
| ...%         | $...                         | .   | .      |
| set ...=     | set ...=  /  setenv ...      | .   | .      |
| ...%         | $...                         | .   | .      |

##### B.2.2-FICHEROS DE CONFIGURACION

|  DOS          |  UNIX            |  VMS       | CMS/CP       |
|---------------|------------------|------------|--------------|
| autoexec.bat  | .chsrc (csh)     | login.com  | profile exec |
|               | .profile (ksh)   |            |              |
        

## 3.- Sistema de Ficheros

### A.-Navegando en los Directorios

|    |  DOS          |  UNIX            |  VMS          | CMS/CP                 | |
|----|---------------|------------------|---------------|------------------------|-|
|dir | dir           | ls -l            | directory     | listdir                | |
|    |               |                  |               | listfile               | |
|.    | dir /v       | ls -lasF         | dir /size=all | . | informacion completa |
|.    | .            | ls -i            | .             | . | pares inodo-fichero  |
|.    | dir /s       | ls -R            | .             | . | listado recursivo    |
|cd  | cd            | cd               | set default   | access                 | |
|.    | cd \         | cd /             | .             | . | ir a la raiz         |
|.    | .            | cd               | cd SYS$LOGIN  | . | ir a tu cuenta       |
|.    | cd ..        | cd ..            | cd ..         | . | ir al anterior       |
|      | .           | pushd            | .             | .                      | |
|      |             | popd             |               |                        | |
|      |             | dirs             |               |                        | |
|      | prompt $p   | echo $cwd        | show default  | q accessed             | |
    

### B.-Analizando Ficheros

  |  DOS    |  UNIX     |  VMS          | CMS/CP       |
  |---------|-----------|---------------|--------------|
  | more <  | more      | {more/most}   | browse       |
  | type    | cat       | type          | type         |
  | .       | tail      | .             | .            |
  | .       | head      | .             | .            |
  | .       | file      | .             | .            |
  | .       | wc -l     | .             | .            |
  | sort    | sort      | .             | sort         |
  | fc      | diff      | differences   | comp         |
  | comp    |           |               |              |

**more**
  |  DOS          |  UNIX        |  VMS       | CMS/CP    |  |
  |---------------|--------------|------------|-----------|--|
  | Ctrl-C        | q            | q          | F3        | salir                |
  | a key         | spacebar     | PgDown     | F8        | siguiente pagina     |
  | .             | b            | PgUp       | F7        | pagina anterior      |
  | .             | enter        | enter      | .         | siguiente linea      |
  | .             | h            | .          | F1        | ayuda                |

    

### C.-Busqueda de/en Ficheros

|  DOS   |  UNIX                   |  VMS     | CMS/CP     |
|--------|-------------------------|----------|------------|
| find   | grep                    | search   | .          |
| dir /s | find . -name "" -print  | .        | .          |
| .      | whereis                 | .        | .          |
| .      | wich                    | .        | .          |
    

### D.-Facilidades en accesos a Ficheros

1.- CAMINOS DE BUSQUEDA (PATH)  
2.- 'LINKS'  

### E.-Modificando el Sistema de Fichero

  |  DOS         |  UNIX     |  VMS              | CMS/CP       |
  |--------------|-----------|-------------------|--------------|
  | md           | mkdir     | create/directory  | create directory       |
  | .            | mkdirhier | create/directory  | .                      |
  | rd           | rmdir     | delete            | erase                  |
  | .            | mknod     | .                 | .                      |
  | del          | rm        | delete            | erase                  |
  | copy         | cp        | copy              | copyfile                     |
  | copy ...+... | cat -o    | .                 | append                       |
  | ren          | mv        | rename            | rename                       |
  | move         | mv        | rename            | movefile                     |
  | .            | touch     | .                 | .                            |
  | copy con     | cat       | .                 | xedit fn1 ft1 fm1 (noscreen  |
    
 * (VMS) purge: igual que delete pero conserva la ultima version del fichero 

    
  |  DOS       |  UNIX  |  VMS  | CMS/CP       |
  |------------|--------|-------|--------------|
  | edlin      | vi     | ls    | xedit        |
  | edit <fn>  | vedit  | edt   |              |
  |            |        | slp   |              |
  |            |        | ...   |              |
    

  |  DOS    |  UNIX     |  VMS          | CMS/CP       |
  |---------|-----------|---------------|--------------|
  | .       | fmt       | .             | .            |
  | .       | split     | .             | .            |
  | .       | expand    | .             | .            |
    

### F.-Atributos

#### F.2.-Uso atributos

  |  DOS   |  UNIX     |  VMS                 | CMS/CP          |
  |--------|-----------|----------------------|-----------------|
  | attrib  | ls -l    | directory/protection | query authority |

    
  |  DOS    |  UNIX     |  VMS                   | CMS/CP           |
  |---------|-----------|------------------------|------------------|
  | .       | umask     | show protection        | .                |
  | attrib  | chmod     | set protection         | GRANT AUTHORITY  |
  |         |           |                        | REVOKE AUTHORITY |
  | .       | umask     | set protection/default |.                 |
    

# 4.- Manejo de Dispositivos
    

### A.-Discos

#### A.1.-Acceso a disco

   |  DOS      |  UNIX   |  VMS           | CMS/CP       |
   |-----------|---------|----------------|--------------|
   | a:        | mount   | .              | link+access  |
   | join      | mount   | .              | .            |
   | subst     | .       | .              | .            |
    

#### A.2.-Manejo de discos

   |  DOS           |  UNIX                     |  VMS                | CMS/CP   |
   |----------------|---------------------------|---------------------|----------|
   | diskcopy a: b: | '/tmp/d00 < /dev/fd0'     | .                   | .        |
   | .              |           +               | .                   | .        |
   | .              | 'cat /tmp/d00 > /dev/fd0' | .                   | .        |
    

### B.-Impresion

   |  DOS      |  UNIX   |  VMS             | CMS/CP       |
   |-----------|---------|------------------|--------------|
   | print     | lpr     | print            | print        |
   | print     | lpq     | sh queue         | q printer    |
   | print /c  | lprm    | .                | .            |
    

### C.-Terminales

  |  DOS           |  UNIX             |  VMS        | CMS/CP    |
  |----------------|-------------------|-------------|-----------|
  | tecla(pausa)   | Control-S         | Control-S   | .         |
  |                | tecla(Bloq Desp)  |             |           |
  | tecla(return)  | Control-Q         | Control-Q   | .         |
  |                | tecla(Bloq Desp)  |             | .         |
  | cls            | Control-L         | .           | CLRSCRN   |
  |                | clear             |             | VMFCLEAR  |
  | .              | .                 | Control-O   | .         |

* tecla(Bloq Desp)  ---> En LINUX
      Control-S          ---> En general
     * Detiene la salida en pantalla de un proceso (para leer poco a poco,  por ejemplo)

* tecla(Bloq Desp)  ---> En LINUX
   Control-Q            ---> En general
     * Continua la salida en pantalla.

* clear
   Control-L
     * Borra la pantalla y situa el cursor en la esquina superior izquierda.
         
----------

