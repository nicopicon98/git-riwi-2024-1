# Patrones de nombres de archivo para `git add`

Git es un sistema de control de versiones distribuido que permite a los desarrolladores colaborar en proyectos de software. Uno de los comandos más utilizados en Git es `git add`, que agrega cambios en el directorio de trabajo al área de preparación (staging area) para ser incluidos en el próximo commit.

### Agregar todos los archivos

```sh
git add .
```

Esto agregará todos los archivos modificados y nuevos en el directorio actual al área de preparación.

o

```sh

git add -A
```

o 

```sh

git add --all
```

o 

```sh

git add -u
```

o 

```sh

git add *
```

La diferencia entre `git add .` y `git add -A` es que el primero no agrega archivos eliminados, mientras que el segundo sí lo hace. `git add -u` solo agrega archivos modificados o eliminados, pero no nuevos archivos. `git add --all` es equivalente a `git add -A`. `git add *` agrega todos los archivos en el directorio actual, incluyendo aquellos que están en subdirectorios. 

## Agregar archivos específicos

### Agregar un archivo específico:

```sh

git add index.html
```

### Agregar todos los archivos que comienzan con "init":

```sh
git add init*
```
Esto agregará archivos como init-config.js, initialize.py, etc., en el directorio actual.

### Agregar todos los archivos .js que se encuentran en cualquier subdirectorio dentro de src/:

```sh

git add src/**/*.js
```

Esta sintaxis es útil para repositorios con estructuras de directorios profundas.

### Agregar todos los archivos que terminan en .test.js para agregar tests específicos de JavaScript:

```sh

git add *.test.js
```

Ideal para cuando solo quieres stagear tus tests después de hacer cambios o añadir nuevos.

### Agregar todos los archivos excepto aquellos que terminan en .log (usando Git Bash o un shell Unix-like):

```sh

git add * | grep -v '\.log$'
```

Primero agregas todo, luego (simbolo "|" que significa "pipe") filtras los archivos que no terminan en .log. 

### Agregar archivos modificados que no sean nuevos (no untracked):

```sh

git add -u
```

Esto solo agrega al stage archivos que ya estaban siendo rastreados y que han sido modificados, excluyendo nuevos archivos (untracked).

### Agregar todos los archivos README.md en cualquier parte del repositorio:

```sh

git add **/README.md
```

Útil para actualizar descripciones o documentación del proyecto en varios lugares.

### Agregar todos los archivos modificados o eliminados, pero no nuevos archivos, en un subdirectorio específico (ej. docs/):

```sh

git add docs/ -u
```
Esto se enfoca en actualizar la documentación existente sin añadir nuevos archivos a la documentación.

### Agregar todos los archivos cuyos nombres contienen un número:

```sh

git add * *[0-9]*
```

o

```sh

git add *0 *1 *2 *3 *4 *5 *6 *7 *8 *9
```

Añadiria archivos como chapter1.md, 2020-logs.txt, etc., útil para cuando los nombres de archivo siguen un patrón numérico standard.


### Agregar todos los #archivos Python modificados recientemente, limitando a los 5 más recientemente modificados (usando Unix-like commands):

``` sh

git ls-files -m | grep '\.py$' | xargs stat --format="%Y %n" | sort -n | cut -d' ' -f 2- | tail -n 5 | xargs git add
```

Este comando es una combinación de comandos Unix y Git para filtrar, ordenar por fecha de modificación, y limitar la cantidad de archivos. Te explicaré paso a paso:

1. `git ls-files -m` lista los archivos modificados. la opción `-m` es para listar solo los archivos modificados.
2. `grep '\.py$'` filtra los archivos que terminan en .py. El backslash `\` es para escapar el punto `.` y `$` es para indicar que el patron que buscamos es al final del nombre del archivo.
3. `xargs stat --format="%Y %n"` obtiene la fecha de modificación y el nombre de archivo de cada archivo. xargs es para pasar la salida de un comando a otro. stat es para obtener información sobre los archivos. `--format="%Y %n"` es para mostrar la fecha de modificación y el nombre del archivo.
4. `sort -n` ordena los archivos por fecha de modificación en orden numérico. sort es para ordenar la salida de un comando. `-n` es para ordenar numéricamente.
5. `cut -d' ' -f 2-` elimina la fecha de modificación, dejando solo el nombre del archivo. `cut` es para cortar partes de una cadena. `-d' '` es para especificar el delimitador como un espacio, y `-f 2-` es para seleccionar la segunda columna y todas las siguientes.
6. `tail -n 5` muestra solo los 5 archivos más recientemente modificados. tail es para mostrar las últimas líneas de la salida. `-n 5` es para mostrar solo las últimas 5 líneas.
7. `xargs git add` agrega los archivos al área de preparación. xargs es para pasar la salida de un comando a otro. Por ejemplo si la salida es `file1.py file2.py file3.py`, xargs ejecutará `git add file1.py file2.py file3.py`. xargs ejecutará `git add` con los nombres de archivo como argumentos.

### Agregar todos los archivos excepto aquellos en un directorio específico (por ejemplo, excluyendo node_modules/):

```sh

git add $(git ls-files -o --exclude-standard | grep -v '^node_modules/')
```

Te explicaré paso a paso:

1. git add: Agrega los archivos al área de preparación.
2. $(...): Ejecuta el comando dentro de los paréntesis y pasa la salida como argumento a git add. O sea, el resultado del comando se convierte en una lista de archivos que se agregan.
3. git ls-files: Lista los archivos no rastreados.
4. -o: Muestra solo los archivos no rastreados.
5. --exclude-standard: Excluye los archivos ignorados por .gitignore.
6. |: Pasa la salida del comando anterior al siguiente comando.
7. grep: Filtra los archivos basados en un patrón. Por ejemplo: git config | grep user.name. filtrará la salida de git config para mostrar solo la línea que contiene user.name.
8. -v: Invierte la búsqueda, mostrando solo las líneas que no coinciden con el patrón.
9. '^node_modules/': El patrón para excluir archivos en el directorio node_modules/. El carácter '^' es para indicar que el patrón debe coincidir al principio de la línea.

Utiliza git ls-files para listar todos los archivos no rastreados (excluyendo los ignorados por .gitignore), filtra aquellos en node_modules/, y los agrega.

```javascript
console.log("hola mundo")
```