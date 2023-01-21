# Introducción a Unix/Linux

### Materiales usados en ARCOS.INF.UC3M.ES con Licencia [CC BY-NC 4.0](http://creativecommons.org/licenses/by-nc/4.0/) 

## Materiales

* Transparencias y videos:

<html>
<ul>
<div class="table-responsive">
    <table class="table table-bordered table-sm table-hover" >
            <tr>
                <th class="col-4" style="width:33vh;">Transparencias</th>
                <th class="col-4" style="width:33vh;">Videos</th>
            </tr>
            <tr>
                <td class="align-middle">
                    <b><a href="https://acaldero.github.io/uc3m_c/slides/clase_w0-ubuntu-instalacion.pdf"><u>Instalación de Ubuntu en VirtualBox</u></a><u></u></b>
                </td>
                <td class="align-middle">
                    <ol>
                        <li> <a href="http://www.youtube.com/watch?embed=no&amp;v=MwfB9lnB0_A&amp;feature=related" target="_blank">Instalación en VirtualBox</a> </li>
                        <li> <a href="http://www.youtube.com/watch?embed=no&amp;v=0An_9Kcv62o&amp;feature=related" target="_blank">Instalación del entorno de desarrollo C</a></li>
                    </ol>
                </td>
            </tr>
            <tr>
                <td class="align-middle">
                    <b><a href="https://acaldero.github.io/uc3m_c/slides/clase_w0-ubuntu-fichydirs.pdf"><u>Uso de ficheros y directorios en Linux</u> </a></b>
                </td>
                <td class="align-middle">
                    <ol>
                        <li> <a href="http://www.youtube.com/watch?embed=no&amp;v=2U5bJKUX_6s&amp;feature=related"
                                target="_blank">El sistema de ficheros desde línea de mandatos</a></li>
                    </ol>
                </td>
            </tr>
            <tr>
                <td class="align-middle">
                    <b><a href="https://acaldero.github.io/uc3m_c/slides/clase_w0-ubuntu-procesos.pdf"><u>Uso de procesos en Linux</u> </a></b>
                </td>
                <td class="align-middle">
                    <ol>
                        <li>  <a href="http://www.youtube.com/watch?embed=no&amp;v=ym3BeppIE8I&amp;feature=related" target="_blank">Gestión de procesos desde línea de mandatos </a></li>
                    </ol>
                </td>
            </tr>
        </tbody>
    </table>
</div>
</ul>
</html>

* Enlaces adicionales:
  * [Jaime Pons |- AprendoLinux](https://www.youtube.com/channel/UCaA0nwerdKCGE7F_doNWdGg)
  * [www.aprendolinux.com](www.aprendolinux.com)


## Introducción a Unix/Linux

### 1.- Comenzando
    
#### A.- Entrar y Salir de la Cuenta

|  DOS   |  UNIX     |  VMS         | CMS/CP       |
|--------|-----------|--------------|--------------|
|  .     |  login    |  .           | logon        |
|  .     |  passwd   | set passwd   | password     |
|  .     | exit      | logout       | logoff       |


* login
    * Mandato que nos permiten entrar en nuestra cuenta.
*  passwd
    * Permite cambiar la contraseña de entrada.
    * El programa te pedirá tu antigua clave (comprueba que eres tú) y también te pedirá la nueva 2 veces (ayuda a evitar poner una contraseña con un carácter mal).
       Si te confundes, presiona Ctrl-C (la tecla control y la letra 'c' a la vez) y vuelve a ejecutar.
```bash
     guernika# passwd
     Changing password for u55555
     Enter old password:
     Enter new password:
     Re-type new password:
     Password changed.
   ```

* exit | logout
   * Permite salir de la cuenta.
   * Usando el comando 'exit' puede indicar que no se puede salir de la cuenta porque queda tareas pendientes.
      Al poner otra vez 'exit' se fuerza a matar las tareas pendientes y salir (en la mayoría de los Unix).
   * También se sale con Control-D, solo en algunos shells.


#### B.- Información de recursos disponibles

|  DOS   |  UNIX     |  VMS         | CMS/CP       |
|--------|-----------|--------------|--------------|
|  .     | quota -v  |  sh quota    | q limits     |
| chkdsk |  df       |  .           | q v stor     |
|  .     |  du       |  .           | .            |
|  .     |  .        |  .           | q disk       |
|  .     |  .        |  .           | q time       |


* quota -v                        
    * Lista la cantidad de recurso asignado a tí y la cantidad ocupado (tiempo, disco, etc.)
    * A partir del límite máximo no te deja guardar nada más, y tendrás el tiempo indicado por timeleft para quitar los (limit-quota) que sobran.

```bash
guernika# quota -v
Disk quotas for u55555(uid 555):
Filesystem usage quota limit timeleft  files quota limit timeleft
/u           683   950  1000              80    95   100
```

* df
    * Lista el espacio total+libre de cada una de las unidades.
* du
    * Lista el espacio que ocupa los fichero en el directorio actual y subdirectorios de este.


#### C.- Obtener ayuda

|  DOS   |  UNIX     |  VMS         | CMS/CP       |
|--------|-----------|--------------|--------------|
| help   | man       |  help        | help         |

* &lt;mandato&gt; --h
    * Se reserva '--h' como opción para la ayuda.
* man &lt;mandato&gt;
    * Presenta informa sobre el comando que se le indique (sintaxis, para que sirve y un montón de cosas más).
    * Permite la opción de usar parámetros y manejar comandos internos:
      - Al llamarlo...:
        * man list                        ---> Lista los comandos de Unix por orden alfabético de los que man tiene ayuda.
        * man -a &lt;cmd&gt; ---> Presenta toda la información que tenga el mismo nombre que <cmd>.
                                                       Conforme se sale de la primera ayuda, se entra en la siguiente relacionada.
        * man -k &lt;cmd&gt; ---> Lista toda los comandos relacionados con <cmd> pero no presenta la ayuda de cada uno,
                                                       como si lo hace la opción -a.
      - Dentro de man... :
        * 'h'     ---> Lista de todas las funciones que hay dentro de man.
        * 'q'     ---> Sale del man.
        * ' '      ---> Siguiente pantalla.


### 2.- Ejecución de comandos

#### A.- Gestión de procesos

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

*  &lt;programa&gt;
     * Para ejecutar un programa, solo hay que poner el nombre y dar enter.
     * Unix lo busca en los directorios de la variable de entorno PATH, en orden.
        Si no está, habrá que poner el nombre completo del programa : /path/nombre_prog

* ps
     * Muestra la lista de procesos con su correspondiente número asociado llamado PID ( Process IDentification )

*  kill -9 &lt;número&gt;
      * Mata un proceso de la lista de procesos identificado por su número asociado (PID)
      * Kill sirve para mandar señales a los procesos.            
        La señal 9, es la de matar. 
        Otras: 
        HUP INT QUIT ILL TRAP IOT FPE KILL USR1 SEGV  USR2 PIPE ALRM TERM CHLD CONT STOP, etc. 

*  Ctrl-z
      * Entiéndase, dar a Ctrl y la tecla de la letra 'z' simultáneamente.
      * Para un proceso (no lo mata, lo deja 'congelado')

* jobs
     * Lista de procesos en espera con su correspondiente orden

*  bg <orden>
     * Hace que un programa en espera se ejecute en background.

* fg <orden>
    * Hace que un programa en espera se ejecute en foreground, por pantalla.

* %&lt;orden&gt;
     * Vuelve al proceso que previamente se había parado ( totalmente equivalente al anterior )
      * En algunas versiones de Unix, se puede poner :
     ```bash
    %<nombre programa a traer a foreground>
   ```

* &lt;programa&gt; &                                      
     * El programa se ejecutara en background
     * Equivalente a:
        *    ejecutar (programa)
        *    pararlo con ctrl z
        *    jobs
        *    bg (orden de programa)

* nohup &lt;programa&gt; &
     * Se ejecuta el programa en background y aunque te salgas de tu cuenta y apagues el terminal!.
      * Es usado cuando vamos a salirnos de la cuenta, por no poder
        esperar por lo que el proceso padre morirá pero el proceso hijo no!. 
        ( es usado para esos ftp's que tardan mucho, pero ojo! si hay mucho que hacen lo mismo, tarda más y
          a lo peor colapsan la máquina, con lo que hay que reinicializarla y se pierde el trabajo. 
          Planificar y si se ve que esta sobrecargado, ¡dejarlo para más tarde! )

* at &lt;hora&gt; &lt;proceso&gt;
     * Para ejecutar un proceso(s) a la hora y día que se quiera!.
        ( para ejecutar mas de un comando, basta con que el proceso sea un shell-script )


#### B.- Interpretes de mandatos: 'shells'

##### B.1.- 'Shells' más sencillos

|  DOS         |  UNIX                            |  VMS     | CMS/CP             |
|--------------|----------------------------------|----------|--------------------|
| dosshell     | .                                | swing    | filelist / dirlist |
| command.com  | bash,csh,ksh,sh,tcsh,zsh,mc,...  | .        | .                  |


*  mc
     * Mightnight Commandant, clónico de comandante norton para Unix.

*  { ash,bash,csh,ksh,msh,sh,tcsh,tsh,zsh,...  } 
     * Interprete de comandos al cual indicar los comandos que queramos ejecutar.


##### B.2.- Personalizar el 'shell'

|  DOS   |  UNIX     |  VMS       | CMS/CP   |
|--------|-----------|------------|----------|
| .      | chsh      | .          | .        |
    

*  chsh
      * Cambia el shell definido en el fichero password que es el que se ejecuta al entrar en tu cuenta
      * Se aconseja el tcsh, pues tiene muchas utilidades:
         - Se puede sacar los comandos metidos anteriormente, como si tuvieras en DOS el DosKey instalado.
         - Si escribes parte del nombre de un fichero (o directorio) y das a tabulador, completa el nombre.
         - Si pones 'set correct=all', cada vez que el crea que te equivocas,
           te presenta el comando mas parecido y pide confirmación para ejecutarlo.
         - Etc.
      * En algunos sistemas, solo lo puede hacer el usuario root.

```bash
guernika>  chsh /bin/tcsh
```
   o bien
   
```bash
guernika> chsh
        (1) /bin/sh
        (2) /bin/csh
        (3) /bin/bash
        (4) /bin/tcsh
        which you want? _4
```

###### B.2.1- VARIABLES DE ENTORNO

|  DOS         |  UNIX                        | VMS | CMS/CP |
|--------------|------------------------------|-----|--------|
| set ...=...  | set ...=... / setenv ... ... | .   | .      |
| ...%         | $...                         | .   | .      |
| set ...=     | set ...=  /  setenv ...      | .   | .      |
| ...%         | $...                         | .   | .      |

   Una variable de entorno es una cadena de caracteres que hace referencia a otra cadena.
   Ejemplo, "saludo=hola", saludo es la variable de entorno que usaremos para referirnos a hola.

   Veamos su manejo con ejemplos de referencia:
* Cómo se definen las variables de entorno:
  * set HOME=/home/u55555
          setenv uname u55555
* Cómo se ver las variables de entorno y su equivalencia:
  * set
     setenv
     env

* Cómo se usa el valor almacenado en la variable (cómo se referencian):
  * cd   $HOME
    echo $uname

* Cómo se borran las variables de entorno: 
  * set HOME=
     setenv uname


###### B.2.2- FICHEROS DE CONFIGURACIÓN

|  DOS          |  UNIX            |  VMS       | CMS/CP       |
|---------------|------------------|------------|--------------|
| autoexec.bat  | .chsrc (csh)     | login.com  | profile exec |
|               | .profile (ksh)   |            |              |
        
Seguramente, las modificaciones echas en el apartado anterior querremos que sean permanentes, 
no tener que teclearlas cada vez que arranquemos la cuenta. 
¿Cómo?, escribiendo los comandos en un fichero llamado:
*  .cshrc   (csh)
*  .profile (ksh)


### 3.- Sistema de ficheros

#### A.- Navegando en los directorios

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
    


* ls &lt;directorio&gt;
   * ls -lasF ---> información completa
   * ls -i       ---> pares inodo-fichero
   * ls -R      ---> listado recursivo

      * Lista los ficheros del directorio que se le pase como argumento
        ( si NO se le pasa argumento, lista el directorio en que nos encontremos en ese preciso momento )
      * Para conseguir un listado 'recursivo' hay varias opciones:
        ls -R                           &lt;dir&gt;
        find . -print -name   &lt;dir&gt;
        du -a                         &lt;dir&gt;
      * Particularidades: en AIX (El Unix de IBM) existe también 'li' y 'di' 

<html>
<pre>
[ls]
>
>   ~/bin/ls -lasF
>
>
>      total bloques en el directorio
>         |
>         |
>
>    |  total 8                                                         |
>    |  1 drwxr-xr-x   4 root     root         1024 Oct 11 01:11 .      |
>    |  1 drwxr-xr-x  18 root     root         1024 Oct 11 01:15 ..     |
>    |  1 drwxr-xr-x   2 root     bin          1024 Oct 11 01:14 bin    |
>    |  5 drwxr-xr-x   2 root     users        5120 Oct 11 01:12 dev    |
>
>       |     |        |   |       |            |    \         /  |
>       |     |        |    \       -----       |      -------    |
>      /      |        |      \          |      |        |        |
> numero  permisos  numero de   dueñ  grupo  tamañ  fecha    nombre
>Bloques            entradas                   fichero           fich/dir
>
>     ** "número de entradas" significa :
>          - si es un directorio, el número de entradas que posee
>            ese directorio. ( el numero de entradas de un directorio
>            es  el número de ficheros mas el número de directorios
>            excluyendo el directorio ".", que es el mismo )
>          - si es un fichero, es el número de entradas de directorio
>            que apuntan a ese fichero ( nodos-i )
>       ** la primera columna depende de la implementacion de Unix.
>          Es el número de bloques. El tamaño de un bloque en unas
>          implementaciones es 1024 bytes y en otras 512 bytes.
>
</pre>
</html>

* cd "&lt;directorio&gt;"
   *  cd /    ---> ir a la raiz
   *  cd      ---> ir a tu cuenta
   *  cd ..   ---> ir al anterior

     * Cambia de directorio.
        Realmente, cambia el contenido de una variable del sistema operativo en la cual guarda el directorio de trabajo, 
        que es aquel que el sistema usara cuando lo omitamos.
      * Hay ciertos detalles a recordar:
        - La \ de dos es la / en Unix:                               
                cd /u/camino/... (ux) ---  cd \u\camino\... (dos)     
        - Para acceder al directorio 'HoLa', vale:
             - cd HoLa                                                
             - cd "HoLa"                                              
        - PERO, si hace mkdir "HoLa ", solo se puede acceder con:   
             - cd "HoLa "

* pwd
   echo $cwd
     * Imprime el Current Working Directory, es decir, el listado de directorios a pasa para ir
       desde la raíz al directorio donde estamos actualmente.

* pushd/popd <directorio>
     * Se crea una pila, en la que se almacena el nombre de los directorios que nosotros queramos, 
        y se permite fácilmente cambiar a uno de los directorios de la pila
        * popd          ---> cuando se ejecute, nos cambiaremos al
                                     directorio situado en cabeza de pila y este desaparece de la cima.
        * pushd        ---> lista todos los componentes de la pila.
                                     (en algunos sistemas, no lista, si intercambia el directorio actual con el cima de pila)
        * pushd &lt;d&gt; ---> inserta un nuevo dir en cima de pila.


#### B.-Analizando Ficheros

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

* more &lt;fichero&gt;
   *  q                 ---> salir
   *  barra espaciadora ---> siguiente pagina
   *  b                 ---> pagina anterior
   *  enter             ---> siguiente linea
   *  h                 ---> ayuda

      * Visualiza el contenido de un fichero, parando cuando se "llene" una pantalla y 
         esperando a que el usuario presione teclas para continuar, o no.

*  cat &lt;fichero&gt;
     * Visualizacion fichero sin pausa.
     * El nombre de cat proviene de "CATenate".
     * Particularidades:
        *  En algunos Unix "&gt; &lt;fichero&gt;" equivale a "cat &gt; &lt;fichero&gt;"

* tail -&lt;número&gt; &lt;fichero&gt;
     * Visualiza las últimas &lt;número&gt; líneas del fichero &lt;fichero&gt;.
     * Si es un fichero al que otro proceso esta añadiendo datos al mismo tiempo entonces usar "tail -f &lt;fichero&gt;".

*  head -&lt;número&gt; &lt;fichero&gt;
     * Visualiza las primeras &lt;número&gt; líneas del fichero &lt;fichero&gt;.

*  file &lt;fichero&gt;
     * Dice a que tipo de fichero pertenece &lt;fichero&gt;:
       * bin   ---> binario, ejecutable
       * ascii ---> texto
       * c       ---> fuente en c
       * ...

* diff &lt;fichero_1&gt; &lt;fichero_2&gt;
     * Compara el contenido de dos ficheros e indica las diferencias que encuentra.

* wc -l &lt;fichero&gt; 
     * Cuenta el número de líneas, palabras, etc. del fichero &lt;fichero&gt; :
        *  wc -c  &lt;fichero&gt; ---> cuenta caracteres.
        *  wc -l   &lt;fichero&gt; ---> cuenta  líneas.
        *  wc -w &lt;fichero&gt; ---> cuenta  palabras.

* sort &lt;...&gt;
     * Ordena items de un fichero.


#### C.- Busqueda de/en Ficheros

|  DOS   |  UNIX                   |  VMS     | CMS/CP     |
|--------|-------------------------|----------|------------|
| find   | grep                    | search   | .          |
| dir /s | find . -name "" -print  | .        | .          |
| .      | whereis                 | .        | .          |
| .      | wich                    | .        | .          |
    

* find <...> --- grep <...> --- SEARCH <...> ---  ???
     * Busca una cadena de caracteres en un fichero.
     * 'grep' es el acronimo de "Global Regular Expression Print"
     * 'grep' no busca la cadena que le pongamos directamente;
        Esa cadena es interpretada como patrón o "expresion regular"
        Ejemplos :
        *   grep pepk fichero  ---> Busca la cadena pepk en fichero
        *   grep [0-9] fichero  ---> Devuelve las líneas que contengan un dígito.              
        *   grep a* fichero       ---> Devuelve las líneas que contengan cadenas de aes.

* find <dir_comienzo_busqueda> -name <nombre_fichero_a_buscar>
     * Usado para buscar donde se encuentra un fichero;
        Si no se indica directorio de comienzo de búsqueda, usa el actual

* whereis &lt;fichero&gt;
     * Igual que el `find', pero busca SOLO ficheros fuentes ( en c ), objetos, y binarios

* which &lt;fichero&gt;
     * Igual que el `find' pero busca SOLO en los directorios especificados en la variable PATH.


#### D.- Facilidades en accesos a Ficheros

1.- CAMINOS DE BUSQUEDA (PATH)  

- En general, es algo asi:
```bash
   PATH=/bin;/usr/bin;~/bin
```

- Se suele usar una variable de entorno especial que contiene una lista de directorios donde buscar dónde está un fichero ejecutable cuando solo le damos al interprete de comandos el nombre del fichero binario.
- En Unix no se busca en el directorio actual por defecto, en DOS si (primero en la búsqueda).


2.- 'LINKS'  o enlaces

 * Un link es una referencia a otro fichero. Si tienes un fichero en un lugar lejano, podrás crearte un fichero en tu cuenta
     que sera una referencia a ese lejano.
* ¿Qué ventaja tiene con respecto a que te lo copies a tu cuenta? ---> al copiartelo hay 2 copias (obvio) en cambio un link solo hay una, y el link es solo una referencia con lo que no "gasta" cuota, ahorrando espacio en disco.

* La sintáxis es:
```bash
# ln [-s] <origen> <nombre>
```
   * Permite referenciar un fichero que esta presente físicamente en otro lugar (&lt;origen&gt;) como si estuviera en el lugar donde esta la referencia (&lt;nombre&gt;).

* Existen dos tipos de enlazado:
	 - El físico o 'duro':
	   * Crea un nodo-i (nueva entrada de directorio) de que apunta al mismo fichero. 
       * Ahora para borrar el fichero, será necesario borrar los dos nombres que lo referencian.
	- El simbólico o 'blando':
	   * Se consigue con la opcion -s. 
	   * El fichero resultante es de tipo 'l', de modo que viene a ser como una "macro" que el sistema operativo sustituye en el comando que tecleemos con ese nombre. 
	   * Por ejemplo:
     ```bash
     lrwxrwxrwx 0 a900000 users 12-1-95 13:30  pek -> /usr/bin/mycmd
     ```
   * cuando tecleemos 'cat pek' el sistema operativo ejecutará 'cat /usr/bin/mycmd' con los permisos de /usr/bin/mycmd.
     Si no tenemos derechos sobre ese fichero, no se visualizará el contenido.
     Pero si nuestro comando solo afecta al enlace (entrada de directorio) y no al propio fichero (como la orden de borrar o mover el fichero) tenemos todos los derechos, pero solo sobre la entrada del enlace en sí misma.

**NOTA**:
 * Los enlaces normales solo pueden hacerse si el enlace a crear está en el mismo dispositivo físico (disco...) que el fichero.
    Si no ocurre así, solo podremos hacer enlaces simbólicos.
 * Los permisos de uso del fichero <destino> no son los que tenga él, sino los que tenga el fichero referenciado (<origen>).
 * Si tenemos un enlace a un fichero de otro usuario/a, si dicho usuario/a lo borra solo borrará su enlace y no el propio fichero, con lo que queda a nuestra disposición pero ocupando espacio suyo!.

#### E.- Modificando el Sistema de Fichero

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
    

* mkdir &lt;directorio&gt;
     * Crea un directorio nuevo, hijo del actual, llamado &lt;directorio&gt;.

* mkdirhier <d1/d2...>
     * Crea varios directorios, al mismo tiempo.
     * Creará el directorio d1 y luego el subdirectorio d2 y así sucesivamente.

* rmdir &lt;directorio&gt;
     * Borra el directorio &lt;directorio&gt;.
     * &lt;directorio&gt; puede ser el path concatenado con el nombre del directorio a borrar.

 ```bash
 guernika$  rmdir /u/primero/u55555/test1
 ```

* mknod &lt;path&gt; &lt;tipo&gt; &lt;princ&gt; &lt;sec&gt;
     * Crea ficheros especiales ( como los del directorio /dev )
     * Donde:
       * &lt;tipo&gt; puede ser:
          * c ( asociado a dispositivo caracter (term))
          * b (     "    "       "     bloque (discos))
       * &lt;princ&gt; es el número de dispositivo hardware (0,1,2...)
       * &lt;sec&gt; es el número de dispositivo secundario asociado a <princ&gt;

        Por ejemplo:
          En Minix y otros sistemas similares en PCs, el diskette lleva el número &lt;princ> igual a 2.
          El segundo número &lt;sec> indica, para el caso del diskette, el tipo de formato (doble densidad, etc) y la unidad.
          Por ejemplo, los discos 3 1/2 HD se codifican con un 28 para la primera unidad de diskette y 29 para la segunda.
          Los 3 1/2 DD llevan los codigos respectivos 16 y 17.

* rm &lt;fichero>
     * Borra el fichero &lt;fichero> ;
        Igual que al borrar directorios, &lt;fichero> puede ser el path y nombre del fichero.
      * Notas :
         - Si no te deja borrar el s.o. , es que según las protecciones, no estás autorizado. Cámbialas y luego intentalo de nuevo	   (ver sección protecciones)
         - De momento, solo en el caso de DOS, es posible "desborrarlo" y recuperarlo con el comando undelete.
         - En Unix se suele simular moviendo el fichero al directorio /tmp. 
           Si se quiere recuperar, se mueve desde /tmp hasta donde estubiera.
           Periodicamente el sysop (responsable del sistema) borra todos los ficheros del /tmp, con lo que son "desborrables" por un periodo de tiempo.
     * Particularidades de algunos Unix:
         * Funciona 'del' o 'erase' también

*  cp &lt;fichero>
      * Copia un fichero: crea otro fichero que tendra el mismo contenido que el original.
      * Notas:
         - Normalmente no se permite que el fichero destino tenga el mismo nombre que el origen.

* cat -o &lt;a> &lt;b> > &lt;a>
     * Concatena el fichero &lt;b> al final del &lt;a&gt;.

* mv &lt;nombre_fichero&gt; &lt;nuevo_nombre&gt;
     * Cambia de nombre un fichero o un directorio.

* mv &lt;ubicación&gt; &lt;nueva_ubicación&gt;
     * Cambia la ubicación de un fichero: lo traslada a otro directorio borrándolo de su posición original.
   * Nota:
        - En los sistemas que no lo implementa se puede simular con la secuencia "rename+delete" o "copy+delete".
   * Ejemplo:
 ```bash
 C:\> move c:\practica\memoria.txt a:\memoria.txt
 ```

* touch -t MMDDhhmm &lt;fichero&gt;
     * Cambia SOLO la fecha de un fichero (la fecha de última modificación del fichero).
        MMDDhhmm es el mes-día-hora-minuto en números y juntos.

* cat > &lt;fichero&gt;
   cat >> &lt;fichero&gt; ---> apendiza.
     * Edita linea a linea (sin retroceso) un fichero;
        Para terminar, teclear el final de fichero (EOF) con 'Ctrl-D'.

* { vi | vedit } &lt;fichero&gt;
     * Edita un fichero (permite cambiar el contenido de un fichero, normalmente de texto).
      * La eleccion del editor depende de muchas cosas, y es algo personal. Los más conocidos son:
              vi            ---> texto simple                                  
              LaText    ---> a lo WordPerfect/WordStar                     
              EMACS  ---> Trabajo con Lisp/C

* fmt -with &lt;ancho&gt;
      * Ajusta el ancho de un texto a la profundidad indicada (&lt;ancho&gt;), conservando las palabras (es decir, no las corta, si no que las pasa a la línea siguiente )
      * Es por tanto un formateador de texto.

* split -b &lt;bytes&gt; &lt;infile&gt;
     * Crea los ficheros que necesite, resultado de partir el fichero de entrada <infile&gt; en ficheros
        de &lt;bytes&gt; bytes de tamaño.

* expand -t&lt;numero&gt; &lt;fichero&gt;
      * Convierte las tabulaciones del fichero '&lt;fichero&gt;' en '&lt;número&gt;' espacios en blanco.


#### F.- Atributos

##### F.1.- Como interpretar los flags

<html>
<pre>
[ls -l]
>
>  /bin/ls -l
>                   --- rwx : lectura,escritura,ejecución.
>                  |
>                 /-\
>          drwxr-xr-x  2 root   root  5120 Oct 11 01:12  devil
>          |\-/\-/\-/
>          | |  |  |
>          | |  |   - permisos para usuarios/as que se conectan a la máquina
>          | |   ----    "       "  usuarios de la máquina
>          |  -------    "       "  el propietario
>          |
>          |    d directorio
>           --- l enlace simbólico
>               - fichero
</pre>
</html>

*   El permiso x en directorios no significa permiso de ejecución sino permiso de acceder al directorio.


##### F.2.-Uso atributos

  |  DOS   |  UNIX     |  VMS                 | CMS/CP          |
  |--------|-----------|----------------------|-----------------|
  | attrib  | ls -l    | directory/protection | query authority |

    
  |  DOS    |  UNIX     |  VMS                   | CMS/CP           |
  |---------|-----------|------------------------|------------------|
  | .       | umask     | show protection        | .                |
  | attrib  | chmod     | set protection         | GRANT AUTHORITY  |
  |         |           |                        | REVOKE AUTHORITY |
  | .       | umask     | set protection/default |.                 |
    

*  ls -l &lt;fichero&gt;
    * Permite ver los "flags" actuales de cada ficheros en dos y Unix si se omite &lt;f&gt;, presenta el listado de todos.

* umask 
    * Permite ver la máscara de proteción usada por defecto.

*  chmod {ugo}x{rwx} <f|d>
    * Cambia los "flags".

* umask &lt;máscara&gt;
    * Define la máscara-patrón ( m ) a usar por chmod/...  por defecto.
      Ojo, la máscara son los permisos que se anularán por defecto (umask 077, pondra por defecto 700 al fichero)


## 4.- Manejo de Dispositivos

#### A.- Discos

##### A.1.- Acceso a disco

   |  DOS      |  UNIX   |  VMS           | CMS/CP       |
   |-----------|---------|----------------|--------------|
   | a:        | mount   | .              | link+access  |
   | join      | mount   | .              | .            |
   | subst     | .       | .              | .            |
    

  El acceso es "transparente":
  solo existe un "árbol" de directorios, si se quiere acceder a un dispositivo (ej. un disquete) hay que leer 
  el sistema de ficheros del disquete y asignarlo a un directorio vacío, de forma que cuando se entre 
  en ese directorio realmente lo que se hace es acceder a la raíz del "árbol" de directorios del disquete.

* mount <dispositivo> <directorio>
     * Une el sistema de ficheros de un disco ( /dev/fd0 , /dev/hd1 , /dev/sd4 ,... ) a un directorio;
        cambiando a ese directorio podemos ver el contenido de la unidad.
     * Notas:  los dispositivo llamados hd__ son discos duros tipo IDE y los llamados sd__ son SCSI
        
*  unmount <directorio> 
     * Desmonta la unidad de disco que este asociada a el directorio <directorio>
      * NOTA: NO SE DEBE RETIRAR UN DISPOSITIVO FÍSICO SI ANTES NO SE DESMONTÓ.


##### A.2.-Manejo de discos

   |  DOS           |  UNIX                     |  VMS                | CMS/CP   |
   |----------------|---------------------------|---------------------|----------|
   | diskcopy a: b: | '/tmp/d00 < /dev/fd0'     | .                   | .        |
   | .              |           +               | .                   | .        |
   | .              | 'cat /tmp/d00 > /dev/fd0' | .                   | .        |
    

Pueden tratarse como si se tratara de un fichero de capacidad limitada.
Por ejemplo:
```bash
  /tmp/d00 < /dev/fd0
  cat /tmp/d00 > /dev/fd0
``` 
   * Permite duplicar un Floppy;
    * Antes del "cat ...", se saca el disco origen y se inserta el destino.


#### B.- Impresión

   |  DOS      |  UNIX   |  VMS             | CMS/CP       |
   |-----------|---------|------------------|--------------|
   | print     | lpr     | print            | print        |
   | print     | lpq     | sh queue         | q printer    |
   | print /c  | lprm    | .                | .            |

    
*  lpr {lp} &lt;f&gt;
      * Envian un fichero a la impresora.
        ( si se esta imprimiendo alguno, pasa a una cola de espera )
* lpq
     * Permite visualizar la cola de impresion.
        ( ficheros imprimiendose y/o en espera de ser impresos)
* lprm &lt;identificador&gt;
    * Borra uno o mas trabajos de la cola de impresion;
        &lt;identificador&gt; es el numero asociado al fichero que aparece en el listado de 'lpq'


#### C.- Terminales

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
         
