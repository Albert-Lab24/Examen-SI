# APUNTES DE SISTEMAS INFORMÁTICOS — BASH

> Comprueba cada comando antes de continuar. En Linux, los nombres distinguen entre mayúsculas y minúsculas: `Archivo.txt` y `archivo.txt` son nombres diferentes.

---

# BLOQUE 1. NAVEGACIÓN Y CONSULTA DEL SISTEMA

## 1. `ls` — Mostrar archivos y directorios

Muestra el contenido del directorio actual.

```bash
ls
```

Opciones habituales:

| Comando | Qué hace |
|---|---|
| `ls` | Muestra archivos y directorios. |
| `ls -a` | Incluye los archivos ocultos. |
| `ls -l` | Muestra información detallada: permisos, propietario, tamaño y fecha. |
| `ls -la` | Combina el listado detallado con la visualización de archivos ocultos. |
| `ls -lh` | Muestra los tamaños en un formato más fácil de leer (KB, MB, etc.). |

Los archivos ocultos suelen tener un punto al principio del nombre, por ejemplo `.config`.

### Cómo interpretar `ls -l`

Ejemplo:

```text
-rwxr-xr-- 1 alumno alumno 120 Nov 3 08:10 prueba.sh
```

La primera parte indica el tipo de elemento y sus permisos:

```text
- | rwx | r-x | r--
    u     g     o
```

- Primer carácter: tipo de elemento. `-` significa archivo normal y `d` significa directorio.
- `u`: permisos del propietario.
- `g`: permisos del grupo.
- `o`: permisos de los demás usuarios.
- `r`: lectura; `w`: escritura; `x`: ejecución; `-`: permiso no concedido.

El resto del listado muestra, entre otros datos, el número de enlaces, propietario, grupo, tamaño, fecha y nombre.

## 2. `man` — Consultar el manual de un comando

Muestra el manual de un comando.

```bash
man ls
man mkdir
man cp
man mv
man chmod
```

Dentro del manual:

| Tecla | Función |
|---|---|
| Flechas arriba/abajo | Desplazarse. |
| `Espacio` | Avanzar una página. |
| `b` | Retroceder una página. |
| `/palabra` | Buscar una palabra. |
| `n` | Ir al siguiente resultado de búsqueda. |
| `q` | Salir del manual. |

Si necesitas conocer las opciones de un comando, puedes consultar su manual con `man nombre_comando`.

## 3. `clear` — Limpiar la pantalla

Limpia visualmente la terminal. No elimina archivos ni borra el historial.

```bash
clear
```

## 4. `history` — Consultar el historial

Muestra los comandos ejecutados anteriormente en la sesión o guardados en el historial del usuario.

```bash
history
```

Para mostrar, por ejemplo, los últimos 10 comandos:

```bash
history 10
```

## 5. `mkdir` — Crear directorios

Crea una carpeta en la ubicación indicada.

```bash
mkdir documentos
```

Crear varias carpetas:

```bash
mkdir documentos scripts copias temporal
```

Crear directorios intermedios con `-p`:

```bash
mkdir -p documentos/texto documentos/informes
```

`-p` permite crear también los directorios padre que todavía no existan y evita un error si el directorio ya existe.

Ejemplo de estructura completa:

```bash
mkdir -p ~/practica_bash/documentos/texto
mkdir -p ~/practica_bash/documentos/informes
mkdir -p ~/practica_bash/scripts
mkdir -p ~/practica_bash/copias
mkdir -p ~/practica_bash/temporal
```

El símbolo `~` representa el directorio personal del usuario.

## 6. `cd` — Cambiar de directorio

Permite moverse entre carpetas.

```bash
cd documentos
```

| Comando | Qué hace |
|---|---|
| `cd documentos` | Entra en `documentos`, dentro de la ubicación actual. |
| `cd ..` | Sube al directorio padre. |
| `cd ~` | Va al directorio personal. |
| `cd` | También va al directorio personal. |
| `cd /` | Va al directorio raíz del sistema. |
| `cd -` | Vuelve al directorio anterior. |

### Rutas relativas y absolutas

- **Ruta relativa:** indica una ubicación desde el directorio actual.
- **Ruta absoluta:** indica la ubicación completa desde la raíz `/`.

Ejemplo de ruta relativa, si estás en `practica_bash`:

```bash
cd documentos/informes
```

Ejemplo de ruta absoluta:

```bash
cd /home/alumno/practica_bash
```

La ruta absoluta concreta depende del usuario y del entorno. Puedes averiguar dónde estás con `pwd`.

## 7. `pwd` — Mostrar la ubicación actual

Muestra la ruta completa del directorio en el que estás.

```bash
pwd
```

Es útil antes de crear, mover o eliminar archivos para comprobar que estás en la ubicación correcta.

## 8. `tree` — Mostrar la estructura en forma de árbol

Muestra las carpetas y archivos de forma jerárquica.

```bash
tree
```

Ejemplo:

```text
practica_bash
├── documentos
│   ├── texto
│   └── informes
├── scripts
├── copias
└── temporal
```

Si aparece `command not found`, significa que `tree` no está instalado en ese entorno. El documento de ejercicios lo utiliza, pero no garantiza que esté instalado en todos los sistemas.

---

# BLOQUE 2. CREACIÓN, EDICIÓN Y CONSULTA DE ARCHIVOS

## 9. `touch` — Crear archivos vacíos

Crea un archivo vacío si todavía no existe.

```bash
touch apuntes.txt
```

Crear varios archivos:

```bash
touch apuntes.txt tareas.txt resumen.txt
```

Crear archivos dentro de una carpeta:

```bash
touch documentos/texto/apuntes.txt
touch documentos/informes/informe1.txt documentos/informes/informe2.txt
```

Si el archivo ya existe, `touch` no borra su contenido: actualiza sus marcas de tiempo.

## 10. `echo` — Mostrar o escribir texto

Muestra texto por pantalla:

```bash
echo "Hola mundo"
```

También se utiliza para escribir texto en archivos mediante redirecciones.

### `>` — Escribir sobrescribiendo

```bash
echo "Primera línea" > apuntes.txt
```

Crea el archivo si no existe. Si ya existe, sustituye todo su contenido por el texto indicado.

### `>>` — Añadir al final

```bash
echo "Segunda línea" >> apuntes.txt
```

Añade el texto al final del archivo sin borrar lo que ya contenía.

Ejemplo para crear un archivo con varias líneas:

```bash
echo "Mi primera práctica de Bash" > apuntes.txt
echo "Mi nombre es Carlos" >> apuntes.txt
echo "Fecha: 03/11/2026" >> apuntes.txt
```

La primera orden sobrescribe o crea el archivo; las siguientes añaden líneas.

**Diferencia que debes recordar:**

| Símbolo | Efecto |
|---|---|
| `>` | Sobrescribe el contenido del archivo. |
| `>>` | Añade contenido al final. |

## 11. `cat` — Mostrar el contenido de archivos

Muestra por pantalla el contenido de un archivo.

```bash
cat apuntes.txt
```

También puede mostrar varios archivos seguidos:

```bash
cat apuntes.txt tareas.txt
```

Diferencia:
- `ls` muestra los nombres de los archivos de una carpeta.
- `cat` muestra el contenido de un archivo.

## 12. `nano` — Editar archivos desde la terminal

Abre un archivo en el editor de texto Nano.

```bash
nano tareas.txt
```

Si el archivo no existe, Nano permite crearlo.

Atajos habituales:

| Atajo | Función |
|---|---|
| `Ctrl + O` | Guardar el archivo. |
| `Enter` | Confirmar el nombre al guardar. |
| `Ctrl + X` | Salir de Nano. |
| `Ctrl + K` | Cortar la línea actual. |
| `Ctrl + U` | Pegar la línea cortada. |
| `Ctrl + W` | Buscar texto. |

Procedimiento para editar:
1. Ejecuta `nano tareas.txt`.
2. Escribe o modifica el contenido.
3. Pulsa `Ctrl + O` y después `Enter` para guardar.
4. Pulsa `Ctrl + X` para salir.
5. Comprueba el contenido con `cat tareas.txt`.

## 13. `rm` — Eliminar archivos

Elimina archivos.

```bash
rm apuntes.txt
```

Eliminar varios archivos:

```bash
rm uno.txt dos.txt tres.txt
```

Opción habitual:

```bash
rm -i apuntes.txt
```

`-i` pregunta antes de eliminar.

Para eliminar un directorio y su contenido se utiliza la opción recursiva:

```bash
rm -r pruebas
```

**Cuidado:** `rm` normalmente elimina directamente; no mueve el archivo a una papelera. Comprueba la ruta y el nombre antes de ejecutarlo.

## 14. `rmdir` — Eliminar directorios vacíos

Elimina un directorio solamente si está vacío.

```bash
rmdir pruebas
```

Si contiene archivos u otros directorios, no podrá eliminarlo. Primero hay que eliminar o mover su contenido.

Ejemplo:

```bash
rm pruebas/uno.txt pruebas/dos.txt
rmdir pruebas
```

Diferencias:

| Comando | Qué elimina |
|---|---|
| `rm archivo.txt` | Un archivo. |
| `rmdir carpeta` | Una carpeta vacía. |
| `rm -r carpeta` | Una carpeta y su contenido. |

## 15. `mv` — Mover o renombrar archivos

Mueve un archivo a otra ubicación:

```bash
mv apuntes.txt copias/
```

Renombra un archivo:

```bash
mv lectura.txt lectura_final.txt
```

Mueve un archivo y le cambia el nombre:

```bash
mv apuntes.txt copias/apuntes_copia.txt
```

`mv` mueve el elemento: deja de estar en la ubicación anterior.

## 16. `cp` — Copiar archivos

Crea una copia y conserva el archivo original.

```bash
cp apuntes.txt copias/
```

Copiar y dar otro nombre a la copia:

```bash
cp apuntes.txt copias/apuntes_copia.txt
```

**Diferencia entre `cp` y `mv`:**

| `cp` | `mv` |
|---|---|
| Copia el archivo. | Mueve el archivo o lo renombra. |
| Conserva el original. | El archivo deja de estar en la ubicación anterior. |
| Quedan dos versiones. | Normalmente queda una versión en la nueva ubicación. |

Si modificas una copia normal, el contenido del original no cambia automáticamente.

---

# BLOQUE 3. PERMISOS DE ARCHIVOS Y SCRIPTS EJECUTABLES

## 17. Permisos de Linux

Linux distingue tres grupos de usuarios:

| Letra | Usuario |
|---|---|
| `u` | Propietario (user). |
| `g` | Grupo (group). |
| `o` | Otros usuarios (others). |
| `a` | Todos (all). |

Hay tres permisos básicos:

| Letra | Permiso | Valor numérico |
|---|---|---:|
| `r` | Lectura (read). | 4 |
| `w` | Escritura (write). | 2 |
| `x` | Ejecución (execute). | 1 |
| `-` | Sin permiso. | 0 |

### Interpretar los permisos

Ejemplo:

```text
-rwxr-xr--
```

Se divide así:

```text
- | rwx | r-x | r--
    u     g     o
```

- `-`: archivo normal.
- `rwx`: el propietario puede leer, escribir y ejecutar.
- `r-x`: el grupo puede leer y ejecutar, pero no escribir.
- `r--`: los demás pueden leer, pero no escribir ni ejecutar.

Si el primer carácter es `d`, se trata de un directorio.

Para consultar permisos:

```bash
ls -l prueba.sh
```

## 18. `chmod` — Modificar permisos

Cambia los permisos de un archivo o directorio.

### Forma simbólica

Estructura:

```bash
chmod QUIEN+/-/=PERMISOS archivo
```

Operadores:

| Símbolo | Significado |
|---|---|
| `+` | Añade permisos. |
| `-` | Quita permisos. |
| `=` | Establece exactamente los permisos indicados para ese grupo. |

Ejemplos:

```bash
chmod u+x prueba.sh
```

Añade ejecución al propietario.

```bash
chmod g-w prueba.sh
```

Quita escritura al grupo.

```bash
chmod o+r prueba.sh
```

Añade lectura a los demás usuarios.

Se pueden establecer varios grupos a la vez:

```bash
chmod u=rwx,g=rx,o=r prueba.sh
```

Resultado:

```text
-rwxr-xr--
```

### Forma numérica

Los valores se suman:

| Permisos | Cálculo | Número |
|---|---:|---:|
| `---` | 0 | 0 |
| `--x` | 1 | 1 |
| `-w-` | 2 | 2 |
| `-wx` | 2 + 1 | 3 |
| `r--` | 4 | 4 |
| `r-x` | 4 + 1 | 5 |
| `rw-` | 4 + 2 | 6 |
| `rwx` | 4 + 2 + 1 | 7 |

Se escriben tres números en este orden: propietario, grupo y otros.

Ejemplo:

```bash
chmod 754 prueba.sh
```

Significa:

| Grupo | Número | Permisos |
|---|---:|---|
| Propietario | 7 | `rwx` |
| Grupo | 5 | `r-x` |
| Otros | 4 | `r--` |

Resultado:

```text
-rwxr-xr--
```

**Truco:** `rwx` = 7, `r-x` = 5 y `r--` = 4. Por tanto, `rwxr-xr--` equivale a `754`.

## 19. Crear, editar y ejecutar un script Bash

Un script es un archivo que contiene instrucciones que Bash ejecuta en orden. Normalmente se guarda con extensión `.sh`.

### Paso 1. Crear el archivo

```bash
touch saludo.sh
```

### Paso 2. Editarlo con Nano

```bash
nano saludo.sh
```

Escribe:

```bash
#!/bin/bash

echo "Bienvenido a mi primer script"
echo "El script se ha ejecutado correctamente"
```

`#!/bin/bash` se llama *shebang*: indica qué intérprete debe utilizarse al ejecutar el archivo directamente.

### Paso 3. Guardar y salir

En Nano:
1. `Ctrl + O`.
2. `Enter`.
3. `Ctrl + X`.

### Paso 4. Dar permiso de ejecución

```bash
chmod u+x saludo.sh
```

### Paso 5. Ejecutar el script

```bash
./saludo.sh
```

`./` indica que el archivo está en el directorio actual.

También se puede ejecutar con Bash:

```bash
bash saludo.sh
```

Esta segunda forma no requiere que el archivo tenga permiso de ejecución, porque se está pasando como archivo a `bash`.

---

# BLOQUE 4. SCRIPTS BASH: VARIABLES, PARÁMETROS Y CONDICIONALES

## 20. Variables

Una variable guarda un valor para poder utilizarlo después.

Declarar variables:

```bash
nombre="Carlos"
curso="Sistemas Informaticos"
```

Mostrar su contenido:

```bash
echo "$nombre"
echo "$curso"
```

Combinar variables en una frase:

```bash
echo "Hola, soy $nombre y estudio $curso"
```

### Reglas importantes

- Al asignar una variable no se ponen espacios alrededor del `=`.

Correcto:

```bash
nombre="Carlos"
```

Incorrecto:

```bash
nombre = "Carlos"
```

- Para obtener el valor de una variable se utiliza `$`.
- Es recomendable poner las variables entre comillas dobles cuando se utilizan como texto o rutas: `"$nombre"`.

### Ejemplo completo

```bash
#!/bin/bash

nombre="Carlos"
curso="Sistemas Informaticos"

echo "Nombre: $nombre"
echo "Curso: $curso"
echo "Hola, soy $nombre y estudio $curso"
```

## 21. Parámetros posicionales: `$1`, `$2`, `$3`...

Los parámetros permiten introducir datos al ejecutar el script, sin tener que modificar su contenido.

| Símbolo | Significado |
|---|---|
| `$1` | Primer parámetro. |
| `$2` | Segundo parámetro. |
| `$3` | Tercer parámetro. |
| `$4` | Cuarto parámetro. |
| `$#` | Número de parámetros recibidos. |
| `$@` | Todos los parámetros recibidos. |

Ejemplo de script `presentacion.sh`:

```bash
#!/bin/bash

nombre=$1
edad=$2

echo "Hola, $nombre"
echo "Tienes $edad años"
```

Ejecución:

```bash
bash presentacion.sh Carlos 18
```

Resultado:

```text
Hola, Carlos
Tienes 18 años
```

En esta ejecución:
- `$1` vale `Carlos`.
- `$2` vale `18`.
- `$#` vale `2`.

Los parámetros se escriben después del nombre del script y separados por espacios.

**Si un parámetro contiene espacios, hay que escribirlo entre comillas:**

```bash
bash script.sh "Juan Carlos" 18
```

Así `"Juan Carlos"` cuenta como un único parámetro.

## 22. `if`, `elif`, `else` y `fi` — Condicionales

Permiten ejecutar instrucciones diferentes dependiendo de si una condición se cumple.

Estructura básica:

```bash
if [ CONDICION ]; then
    # Instrucciones si la condición es verdadera
else
    # Instrucciones si la condición es falsa
fi
```

Significado:
- `if`: inicia la condición.
- `[ ... ]`: contiene la condición que se comprueba.
- `then`: inicia las instrucciones que se ejecutan si se cumple.
- `else`: inicia las instrucciones alternativas.
- `fi`: cierra el condicional.

Ejemplo:

```bash
edad=18

if [ "$edad" -ge 18 ]; then
    echo "Mayor de edad"
else
    echo "Menor de edad"
fi
```

### `elif` — Comprobar otra condición

Se utiliza para añadir alternativas.

```bash
if [ CONDICION1 ]; then
    echo "Resultado 1"
elif [ CONDICION2 ]; then
    echo "Resultado 2"
else
    echo "Ninguna de las anteriores"
fi
```

Bash comprueba las condiciones en orden. Ejecuta el primer bloque cuya condición sea verdadera.

## 23. Operadores de comparación numérica

Se utilizan dentro de condiciones para comparar números enteros.

| Operador | Significado |
|---|---|
| `-eq` | Igual que. |
| `-ne` | Distinto de. |
| `-gt` | Mayor que. |
| `-lt` | Menor que. |
| `-ge` | Mayor o igual que. |
| `-le` | Menor o igual que. |

Ejemplos:

```bash
[ "$a" -eq "$b" ]  # a es igual a b
[ "$a" -ne "$b" ]  # a es distinto de b
[ "$a" -gt "$b" ]  # a es mayor que b
[ "$a" -lt "$b" ]  # a es menor que b
[ "$a" -ge "$b" ]  # a es mayor o igual que b
[ "$a" -le "$b" ]  # a es menor o igual que b
```

Ejemplo completo:

```bash
#!/bin/bash

num1=$1
num2=$2

if [ "$num1" -gt "$num2" ]; then
    echo "El primer numero es mayor"
elif [ "$num1" -lt "$num2" ]; then
    echo "El primer numero es menor"
else
    echo "Los numeros son iguales"
fi
```

## 24. Comprobar archivos, directorios y permisos

Estas pruebas se utilizan dentro de los corchetes de un `if`.

| Prueba | Qué comprueba |
|---|---|
| `-f ruta` | La ruta existe y es un archivo normal. |
| `-d ruta` | La ruta existe y es un directorio. |
| `-e ruta` | La ruta existe. |
| `-x ruta` | El usuario que ejecuta el script tiene permiso de ejecución sobre la ruta. |
| `-r ruta` | El usuario que ejecuta el script tiene permiso de lectura. |
| `-w ruta` | El usuario que ejecuta el script tiene permiso de escritura. |

Ejemplo: comprobar si existe un archivo normal.

```bash
if [ -f "archivo.txt" ]; then
    echo "El archivo existe"
else
    echo "El archivo no existe o no es un archivo normal"
fi
```

Ejemplo: comprobar si existe un directorio.

```bash
if [ -d "documentos" ]; then
    echo "El directorio existe"
else
    echo "El directorio no existe"
fi
```

Ejemplo: comprobar si existe una ruta.

```bash
if [ -e "ruta" ]; then
    echo "La ruta existe"
else
    echo "La ruta no existe"
fi
```

Ejemplo: comprobar permiso de ejecución.

```bash
if [ -x "saludo.sh" ]; then
    echo "Tiene permiso de ejecucion"
else
    echo "No tiene permiso de ejecucion"
fi
```

**Diferencia importante:** `-e` comprueba que exista la ruta; `-f` comprueba que sea un archivo normal; `-d` comprueba que sea un directorio.

## 25. Negar una condición con `!`

El símbolo `!` invierte el resultado de una condición.

```bash
if [ ! -f "$archivo" ]; then
    echo "No existe como archivo normal"
fi
```

Se lee: «si NO es un archivo normal».

Otro ejemplo:

```bash
if [ ! -d "$destino" ]; then
    echo "El directorio de destino no existe"
fi
```

## 26. Combinar condiciones con `&&` y `||`

Son operadores lógicos:

- `&&`: Y lógico. Las dos condiciones deben cumplirse.
- `||`: O lógico. Basta con que se cumpla una de las condiciones.

Ejemplo con `&&`:

```bash
if [ -f "$archivo" ] && [ -x "$archivo" ]; then
    echo "Es un archivo y tiene permiso de ejecucion"
fi
```

Ejemplo con `||`:

```bash
if [ -f "$ruta" ] || [ -d "$ruta" ]; then
    echo "La ruta es un archivo o un directorio"
fi
```

## 27. Comillas simples y dobles

Comillas dobles: permiten que Bash sustituya las variables por sus valores.

```bash
nombre="Carlos"
echo "Hola $nombre"
```

Resultado:

```text
Hola Carlos
```

Comillas simples: muestran el texto literalmente, sin sustituir variables.

```bash
echo 'Hola $nombre'
```

Resultado:

```text
Hola $nombre
```

**Consejo:** utiliza comillas dobles alrededor de variables que contengan rutas o texto. Así se manejan correctamente los espacios.

## 28. Espacios en los condicionales

Los espacios alrededor de los corchetes son obligatorios.

Correcto:

```bash
if [ "$numero" -gt 0 ]; then
    echo "Positivo"
fi
```

Incorrecto:

```bash
if ["$numero" -gt 0]; then
    echo "Positivo"
fi
```

Tiene que haber un espacio después de `[` y antes de `]`.

---

# BLOQUE 5. EJERCICIOS DE INTEGRACIÓN

Esta parte reúne los patrones de código que se utilizan en los ejercicios 17 al 24. Conviene comprenderlos, porque los ejercicios combinan las mismas instrucciones.

## 29. Comprobar que se han recibido exactamente dos parámetros (ejercicio 17)

```bash
#!/bin/bash

if [ "$#" -eq 2 ]; then
    echo "Parametro 1: $1"
    echo "Parametro 2: $2"
else
    echo "Uso correcto: bash comprobar_parametros.sh nombre edad"
fi
```

Explicación:
1. `$#` cuenta los parámetros.
2. `-eq 2` comprueba que hay exactamente dos.
3. Si se cumple, muestra `$1` y `$2`.
4. Si no, muestra cómo debe ejecutarse.

Pruebas:

```bash
bash comprobar_parametros.sh
bash comprobar_parametros.sh Carlos
bash comprobar_parametros.sh Carlos 18
bash comprobar_parametros.sh Carlos 18 Madrid
```

Solo la tercera ejecución recibe exactamente dos parámetros.

## 30. Comparar dos números (ejercicio 18)

Archivo: `comparar.sh`

```bash
#!/bin/bash

num1=$1
num2=$2

if [ "$num1" -gt "$num2" ]; then
    echo "El primer numero es mayor"
elif [ "$num1" -lt "$num2" ]; then
    echo "El primer numero es menor"
else
    echo "Los numeros son iguales"
fi
```

Pruebas:

```bash
bash comparar.sh 10 5
bash comparar.sh 3 8
bash comparar.sh 7 7
```

Se utilizan:
- `$1` y `$2`: recoger los números.
- `-gt`: mayor que.
- `-lt`: menor que.
- `else`: si no es mayor ni menor, son iguales.

El ejercicio pide probar al menos cinco combinaciones que incluyan las tres situaciones posibles.

## 31. Comprobar si una ruta es un archivo, un directorio o no existe (ejercicio 19)

Archivo: `comprobar_archivo.sh`

```bash
#!/bin/bash

ruta=$1

if [ -f "$ruta" ]; then
    echo "Es un archivo"
elif [ -d "$ruta" ]; then
    echo "Es un directorio"
else
    echo "La ruta no existe o no es un archivo ni directorio"
fi
```

Explicación:
1. Guarda el primer parámetro en `ruta`.
2. `-f` comprueba si es un archivo normal.
3. `-d` comprueba si es un directorio.
4. Si ninguna se cumple, muestra el último mensaje.

Prueba con un archivo real, un directorio real y una ruta inexistente.

## 32. Clasificar un número (ejercicio 20)

Archivo: `clasificar_numero.sh`

```bash
#!/bin/bash

numero=$1

if [ "$numero" -gt 0 ]; then
    echo "El numero es positivo"
elif [ "$numero" -lt 0 ]; then
    echo "El numero es negativo"
else
    echo "El numero es cero"
fi
```

Pruebas:

```bash
bash clasificar_numero.sh 5
bash clasificar_numero.sh -3
bash clasificar_numero.sh 0
```

## 33. Añadir texto a un archivo si existe (ejercicio 21)

Archivo: `gestionar_archivo.sh`

Parámetros:
- `$1`: ruta del archivo.
- `$2`: texto que se añadirá.

```bash
#!/bin/bash

archivo=$1
texto=$2

if [ -f "$archivo" ]; then
    echo "$texto" >> "$archivo"
    echo "Texto añadido correctamente"
else
    echo "El archivo no existe"
fi
```

Ejecución:

```bash
bash gestionar_archivo.sh apuntes.txt "Hola mundo"
```

Las comillas en `"Hola mundo"` hacen que el texto completo se reciba como un solo segundo parámetro. `>>` añade el texto al final del archivo.

## 34. Comprobar si un archivo tiene permiso de ejecución (ejercicio 22)

Archivo: `permisos_archivo.sh`

```bash
#!/bin/bash

archivo=$1

if [ -e "$archivo" ]; then
    if [ -x "$archivo" ]; then
        echo "El archivo tiene permiso de ejecucion"
    else
        echo "El archivo no tiene permiso de ejecucion"
    fi
else
    echo "El archivo no existe"
fi
```

Explicación:
1. `-e` comprueba primero si la ruta existe.
2. Si existe, `-x` comprueba si el usuario que ejecuta el script tiene permiso de ejecución.
3. Si no existe, muestra un mensaje de error.

Hay un `if` dentro de otro `if`: esto se llama condicional anidado.

## 35. Copia de seguridad (ejercicio 23)

Archivo: `copia_seguridad.sh`

Parámetros:
- `$1`: ruta del archivo de origen.
- `$2`: ruta del directorio de destino.

```bash
#!/bin/bash

origen=$1
destino=$2

if [ "$#" -ne 2 ]; then
    echo "Error: debes introducir exactamente dos parametros"
elif [ ! -f "$origen" ]; then
    echo "Error: el origen no existe o no es un archivo normal"
elif [ ! -d "$destino" ]; then
    echo "Error: el directorio de destino no existe"
else
    cp "$origen" "$destino"
    echo "Copia de seguridad realizada correctamente"
fi
```

Explicación, en orden:
1. `-ne 2` comprueba que el número de parámetros sea distinto de dos. Si lo es, muestra un error.
2. `! -f` comprueba que el origen NO sea un archivo normal.
3. `! -d` comprueba que el destino NO sea un directorio.
4. Si todas las comprobaciones se superan, `cp` copia el archivo.
5. Muestra un mensaje de éxito.

Ejemplo:

```bash
bash copia_seguridad.sh apuntes.txt copias
```

## 36. Proyecto final: organizador de documentos (ejercicio 24)

Archivo: `organizador.sh`

**Importante sobre el enunciado:** primero dice que el script recibe la ruta de origen y la ruta de destino, pero después indica que el archivo que se copiará se proporciona como tercer parámetro. El ejemplo siguiente interpreta que se necesitan tres parámetros:
- `$1`: directorio de origen.
- `$2`: directorio de destino.
- `$3`: nombre del archivo que se copiará desde el directorio de origen.

```bash
#!/bin/bash

origen=$1
destino=$2
archivo=$3

if [ "$#" -ne 3 ]; then
    echo "Error: debes introducir tres parametros"
elif [ ! -d "$origen" ]; then
    echo "Error: el directorio de origen no existe"
elif [ ! -d "$destino" ]; then
    echo "Error: el directorio de destino no existe"
elif [ ! -f "$origen/$archivo" ]; then
    echo "Error: el archivo no existe en el directorio de origen"
else
    echo "Contenido del directorio de origen:"
    ls "$origen"

    cp "$origen/$archivo" "$destino"

    echo "Archivo copiado correctamente"
fi
```

Ejemplo:

```bash
bash organizador.sh documentos copias apuntes.txt
```

En este ejemplo:
- `origen` vale `documentos`.
- `destino` vale `copias`.
- `archivo` vale `apuntes.txt`.

La ruta de origen del archivo se construye como `"$origen/$archivo"`, que en este caso equivale a `documentos/apuntes.txt`.

El script comprueba los parámetros y las rutas, muestra el contenido del origen y copia el archivo indicado al destino.

---

# TABLAS DE CONSULTA RÁPIDA

## A. Todos los comandos de la batería

| Comando | Función |
|---|---|
| `ls` | Mostrar archivos y directorios. |
| `man` | Consultar el manual. |
| `clear` | Limpiar la pantalla. |
| `history` | Mostrar el historial. |
| `mkdir` | Crear directorios. |
| `cd` | Cambiar de directorio. |
| `tree` | Mostrar la estructura en árbol. |
| `touch` | Crear archivos vacíos. |
| `echo` | Mostrar o escribir texto. |
| `cat` | Mostrar el contenido de archivos. |
| `nano` | Editar archivos en la terminal. |
| `rm` | Eliminar archivos. |
| `rmdir` | Eliminar directorios vacíos. |
| `mv` | Mover o renombrar. |
| `cp` | Copiar archivos. |
| `chmod` | Cambiar permisos. |
| `bash` | Ejecutar scripts con Bash. |
| `pwd` | Mostrar la ruta actual. |

## B. Operadores de comparación numérica

| Operador | Significado |
|---|---|
| `-eq` | Igual. |
| `-ne` | Distinto. |
| `-gt` | Mayor. |
| `-lt` | Menor. |
| `-ge` | Mayor o igual. |
| `-le` | Menor o igual. |

## C. Pruebas de archivos y permisos

| Prueba | Significado |
|---|---|
| `-f` | Existe y es un archivo normal. |
| `-d` | Existe y es un directorio. |
| `-e` | Existe la ruta. |
| `-x` | El usuario que ejecuta el script tiene permiso de ejecución. |
| `-r` | El usuario que ejecuta el script tiene permiso de lectura. |
| `-w` | El usuario que ejecuta el script tiene permiso de escritura. |

## D. Parámetros y estructuras de Bash

| Elemento | Significado |
|---|---|
| `$1` | Primer parámetro. |
| `$2` | Segundo parámetro. |
| `$3` | Tercer parámetro. |
| `$#` | Número de parámetros. |
| `$@` | Todos los parámetros. |
| `if` | Inicia un condicional. |
| `then` | Inicia el bloque si se cumple la condición. |
| `elif` | Comprueba otra condición. |
| `else` | Bloque alternativo. |
| `fi` | Cierra el condicional. |
| `&&` | Y lógico. |
| `||` | O lógico. |
| `!` | Niega una condición. |

## E. Permisos numéricos

| Número | Permisos |
|---:|---|
| 0 | `---` |
| 1 | `--x` |
| 2 | `-w-` |
| 3 | `-wx` |
| 4 | `r--` |
| 5 | `r-x` |
| 6 | `rw-` |
| 7 | `rwx` |

Orden de los tres números en `chmod`: **propietario, grupo, otros**.

Ejemplo: `chmod 754 archivo.sh` significa propietario `rwx`, grupo `r-x`, otros `r--`.

## F. Símbolos importantes

| Símbolo | Significado |
|---|---|
| `$` | Expande una variable o parámetro. |
| `#` | Inicia un comentario en un script; en `$#` representa el número de parámetros. |
| `=` | Asigna un valor a una variable. |
| `>` | Sobrescribe un archivo. |
| `>>` | Añade al final de un archivo. |
| `!` | Niega una condición. |
| `&&` | Y lógico. |
| `||` | O lógico. |
| `"` | Agrupa texto y permite expandir variables. |
| `'` | Agrupa texto literalmente, sin expandir variables. |
| `.` | Representa el directorio actual cuando se usa en `./archivo`. |
| `/` | Separa directorios en una ruta. |
| `~` | Representa el directorio personal. |

---

# ERRORES TÍPICOS QUE DEBES EVITAR

1. **Olvidar los espacios en los corchetes.**

   Correcto: `if [ "$numero" -gt 0 ]; then`

   Incorrecto: `if ["$numero" -gt 0]; then`

2. **Poner espacios al asignar variables.**

   Correcto: `nombre="Carlos"`

   Incorrecto: `nombre = "Carlos"`

3. **Confundir `>` y `>>`.**

   - `>` sobrescribe.
   - `>>` añade al final.

4. **Confundir `cp` y `mv`.**

   - `cp` conserva el original.
   - `mv` mueve o renombra.

5. **Intentar borrar una carpeta no vacía con `rmdir`.**

   `rmdir` solo elimina directorios vacíos.

6. **Olvidar dar permiso de ejecución a un script.**

   Para ejecutarlo directamente:

   ```bash
   chmod u+x script.sh
   ./script.sh
   ```

7. **Olvidar cerrar un condicional con `fi`.**

8. **Olvidar las comillas cuando un parámetro contiene espacios.**

   Ejemplo:

   ```bash
   bash gestionar_archivo.sh apuntes.txt "Texto que quiero añadir"
   ```

9. **No comprobar la ubicación antes de operar.**

   Utiliza `pwd` para saber dónde estás y `ls` para comprobar el contenido.

10. **No comprobar los resultados.**

    Después de crear, mover, copiar o eliminar, utiliza `ls`, `cat` o `tree` según corresponda.

---

# PLANTILLA GENERAL PARA UN SCRIPT

Puedes utilizar esta estructura como punto de partida para muchos ejercicios:

```bash
#!/bin/bash

# Recoger parametros
parametro1=$1
parametro2=$2

# Comprobar numero de parametros
if [ "$#" -ne 2 ]; then
    echo "Error: numero de parametros incorrecto"
elif [ ! -f "$parametro1" ]; then
    echo "Error: el archivo no existe"
else
    echo "Operacion realizada"
fi
```

No todos los scripts necesitan exactamente estas comprobaciones: adapta la plantilla a lo que pida el enunciado.

---

# RECORDATORIO: CREAR Y EJECUTAR UN SCRIPT

```bash
touch nombre.sh
nano nombre.sh
```

Escribir el código, guardar con `Ctrl + O`, `Enter` y salir con `Ctrl + X`.

Después:

```bash
chmod u+x nombre.sh
./nombre.sh
```

También puedes ejecutarlo así:

```bash
bash nombre.sh
```