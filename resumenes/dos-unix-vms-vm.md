



# Sistemas operativos

## 1.- Comenzando
    
### A.-Entrar y Salir de la Cuenta

|  DOS   |  UNIX     |  VMS         | CMS/CP       |
|--------|-----------|--------------|--------------|
|  .     |  login    |  .           | logon        |
|  .     |  passwd   | set passwd   | password     |
|  .     | exit      | logout       | logoff       |


### B.-Informacion de Recursos disponibles

|  DOS   |  UNIX     |  VMS         | CMS/CP       |
|--------|-----------|--------------|--------------|
|  .     | quota -v  |  sh quota    | q limits     |
| chkdsk |  df       |  .           | q v stor     |
|  .     |  du       |  .           | .            |
|  .     |  .        |  .           | q disk       |
|  .     |  .        |  .           | q time       |

### C.-Optener Ayuda

|  DOS   |  UNIX     |  VMS         | CMS/CP       |
|--------|-----------|--------------|--------------|
| help   | man       |  help        | help         |

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
| command.com  | ash,bash,csh,ksh,sh,tcsh,zsh,... | .        | .                  |
    

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

 
----------

