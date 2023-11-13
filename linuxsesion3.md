# Ejercicos Linux Sesion 3
*Ejercicio 1:* *`Escriba, al menos, cinco variables de entorno junto con el valor que tienen.`*
```bash
~$ variable1=1
~$ variable2=2
~$ variable3=3
~$ variable1=1
~$ variable1=1
```
*Ejercicio 2. `Ejecute las órdenes del cuadro e indique qué ocurre y cómo puede resolver la situación para que la variable NOMBRE se reconozca en el shell hijo.`*
```bash
~$ NOMBRE=FS
~$ echo $NOMBRE
FS
~$ export NOMBRE
~$ bash
~$ echo $NOMBRE
FS
```
*Ejercicio 3: `Compruebe qué ocurre en las expresiones del ejemplo anterior si se quitan las comillas dobles del final y se ponen después de los dos puntos. ¿Qué sucede si se sustituyen las comillas dobles por comillas simples?`*
```bash
~$ echo "Los archivos que hay en el directorio son: $(ls -l)"
Al escribir esa línea como resultado se ve la frase escrita después del echo hasta : y ejecuta el comando ls -l
~$ echo "Los archivos que hay en el directorio son: 'ls -l'"
Al escribir esa línea como resultado se ve la frase escrita después del echo hasta el final y  no se ejecuta el comando ls -l
~$ echo Los archivos que hay en el directorio son: "$(ls -l)"
Al cambiar las "" a después de : se sigue viendo la frase hasta los : y ejecutando el comando ls -l
~$ echo Los archivos que hay en el directorio son: "'ls -l'"
Al cambiar las "" a después de : se sigue viendo la frase exactamente igual que si las "" englovaran la frase entera
~$ echo 'Los archivos que hay en el directorio son: $(ls -l)'
Al escribir esa línea como resultado se ve la frase escrita después del echo al completo y no se ejecuta el comando ls -l
~$ echo 'Los archivos que hay en el directorio son: 'ls -l''
Al escribir esa línea como resultado se ve la frase escrita después del echo al completo, sin que se vena las comillas simples de 'ls -l' y sin ejecutar el comando. 
```
*Ejercicio 4: `Pruebe la siguiente asignación:`* 
```bash
 $ numero=$numero + 1 
 $ echo $numero
 ```
*`¿Qué ha ocurrido?`*
```
Al hacer esa asignación primero me dice que no ha encontrado la orden "+" y cuando visualizo la variable no hay nada.
```
*Ejercicio 5: `Construya un guion que acepte como argumento una cadena de texto (por ejemplo, su nombre) y que visualice en pantalla la frase Hola y el nombre dado como argumento.`*
```bash
#!/bin/bash

# Pedimos al usuario que introduzca su nombre
echo -n "Introduce tu nombre: "

# Guardamos el nombre introducido en una variable
read nombre

# Imprimimos en pantalla "Hola" y el nombre introducido
echo "Hola $nombre"
```
`Otra forma de hacerlo sería:`
```bash
#!/bin/bash

echo "Hola $1"
```

*Ejercicio 6: `Varíe el guion anterior para que admita una lista de nombres.`*
```bash
#!/bin/bash

# Pedimos al usuario que introduzca una lista de nombres
echo -n "Introduce una lista de nombres (separada por espacios): "

# Guardamos los nombres introducidos en una variable
read nombres

# Imprimimos en pantalla "Hola" y los nombres introducidos
# Utilizo un bucle para leer la lista de nombres y poder poner un hola por cada nombre.
for nombre in $nombres; do
echo "Hola $nombre"
done
```
`Otra forma de hacerlo sería:`
```bash
#!/bin/bash

echo "Hola $*"
```
*Ejercicio 7: `Cree tres variables llamadas VAR1, VAR2 y VAR3 con los siguientes valores respectivamente “hola”, “adios” y “14”.`*
```bash
VAR1=hola VAR2=adios VAR3=14
```
`a) Imprima los valores de las tres variables en tres columnas con 15 caracteres de ancho.`
```bash
printf "%-15s %-15s %-15s\n" "$VAR1" "$VAR2" "$VAR3"
```
`b) ¿Son variables locales o globales?`
```
Son variables locales ya que se han creado en el terminal actual.
```
`c) Borre la variable VAR2.`
```bash
unset VAR2
```
`d) Abra otra ventana de tipo terminal, ¿puede visualizar las dos variables restantes?`
```
No se puden visualizar ya que habían sido creadas en el termial actual en su momento y son variables locales. Habría que exportarlas para verlas desde un nuevo terminal.
```
`e) Cree una variable de tipo vector con los valores iniciales de las tres variables.`
```bash
vector=("$VAR1" "$VAR2" "$VAR3")
```
`f) Muestre el segundo elemento del vector creado en el apartado e.`
```bash
echo "${vector[1]}"
```
*Ejercicio 8: `Cree un alias que se llame ne (nombrado así para indicar el número de elementos) y que devuelva el número de archivos que existen en el directorio actual.`* 
```bash
alias ne='echo $(ls -1 | wc -l)'
```
*`¿Qué cambiaría si queremos que haga lo mismo pero en el directorio home correspondiente al usuario que lo ejecuta?`*
```bash
alias ne='echo $(ls -1 ~ | wc -l)'
```
*`Ejercicio 9: Indique la línea de orden necesaria para buscar todos los archivos a partir del directorio home que tengan un tamaño menor de un bloque.`* 
```bash
find ~/ -type f -size -1k
```
*`¿Cómo la modificaría para que además imprima el resultado en un archivo que se cree dentro del directorio donde nos encontremos y que se llame archivosP?`*
```bash
find ~/ -type f -size -1k > archivosP
```
*Ejercicio 10: `Indique cómo buscaría todos aquellos archivos del directorio actual que contengan la palabra “ejemplo”.`*
```bash
grep -rl "ejemplo" .
```
*Ejercicio 11: `Complete la información de find y grep utilizando para ello la orden man`*
```bash
man find

This manual page documents the GNU version of find. GNU find searches the directory tree rooted at each given file name by evaluating the given expression from left to right, according to the rules of precedence (see section OPERATORS), until the outcome is known (the left hand side is false for and operations, true for or), at which point find moves on to the next file name.

If you are using find in an environment where security is important (for example if you are using it to search directories that are writable by other users), you should read the "Security Considerations" chapter of the findutils documentation, which is called Finding Files and comes with findutils. That document also includes a lot more detail and discussion than this manual page, so you may find it a more useful source of information.

man grep

grep searches for PATTERNS in each FILE.  PATTERNS is one or more
patterns separated by newline characters, and grep prints each
line that matches a pattern.  Typically PATTERNS should be quoted
when grep is used in a shell command.

A FILE of “-” stands for standard input.  If no FILE is given,
recursive searches examine the working directory, and
nonrecursive searches read standard input.
```
*Ejercicio 12: `Indique cómo buscaría si un usuario dispone de una cuenta en el sistema.`*
```bash
grep "^juan:" /etc/passwd
```
*Ejercicio 13: `Indique cómo contabilizar el número de ficheros de la propia cuenta de usuario que no tengan permiso de lectura para el resto de usuarios.`*
```bash
find ~ -type f ! -readable | wc -l
```
*Ejercicio 14. `Modifique el ejercicio 8 de forma que, en vez de un alias, sea un guion llamado numE el que devuelva el número de archivos que existen en el directorio que se le pase como argumento.`*
```bash
nano numE

#!/bin/bash
num_archivos=$(find "$1" -maxdepth 1 -type f | wc -l)

echo "El número de archivos en $1 es: $num_archivos"
```