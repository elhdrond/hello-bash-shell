# SCRIPTING

## Posibles correcciones (ten en cuenta que pueden variar dependiendo de tu sistema operativo y directorios existentes)

1. Crea un script que imprima en pantalla: Hola mundo desde Bash.

```bash
#!/bin/bash
# Nombre: hola_mundo.sh
# Descripción: Script que imprime "Hola mundo desde Bash"

echo "Hola mundo desde Bash"
```

Crear y ejecutar el script:
```bash
# Crear el archivo
nano hola_mundo.sh

# Copiar el contenido del script anterior
# Guardar: Ctrl + O, Enter, Ctrl + X

# Dar permisos de ejecución
chmod +x hola_mundo.sh

# Ejecutar el script
./hola_mundo.sh

# O ejecutar sin permisos de ejecución
bash hola_mundo.sh
```

2. Crea un script que muestre la fecha y el directorio actual.

```bash
#!/bin/bash
# Nombre: fecha_directorio.sh
# Descripción: Muestra la fecha actual y el directorio de trabajo

echo "=== Información del Sistema ==="
echo "Fecha y hora actual:"
date

echo ""
echo "Directorio actual:"
pwd

# Alternativa con formato más personalizado
echo ""
echo "=== Información Detallada ==="
echo "Fecha: $(date '+%d/%m/%Y')"
echo "Hora: $(date '+%H:%M:%S')"
echo "Directorio: $(pwd)"
```

Crear y ejecutar el script:
```bash
nano fecha_directorio.sh
chmod +x fecha_directorio.sh
./fecha_directorio.sh
```

3. Crea un script que guarde tu nombre en una variable y lo muestre en pantalla.

```bash
#!/bin/bash
# Nombre: mi_nombre.sh
# Descripción: Guarda un nombre en una variable y lo muestra

# Declarar la variable
nombre="Juan Pérez"

# Mostrar el contenido de la variable
echo "Mi nombre es: $nombre"

# Alternativa con más información
echo "Hola, mi nombre es ${nombre}"
echo "Bienvenido/a, ${nombre}!"

# También puedes usar comillas simples para texto literal
echo 'El nombre guardado es:' "$nombre"
```

Crear y ejecutar el script:
```bash
nano mi_nombre.sh
chmod +x mi_nombre.sh
./mi_nombre.sh
```

4. Crea un script que declare dos variables numéricas, las sume, reste y multiplique, mostrando el resultado de cada operación.

```bash
#!/bin/bash
# Nombre: operaciones.sh
# Descripción: Realiza operaciones matemáticas básicas

# Declarar dos variables numéricas
num1=15
num2=5

echo "=== Operaciones Matemáticas ==="
echo "Primer número: $num1"
echo "Segundo número: $num2"
echo ""

# Suma
suma=$((num1 + num2))
echo "Suma: $num1 + $num2 = $suma"

# Resta
resta=$((num1 - num2))
echo "Resta: $num1 - $num2 = $resta"

# Multiplicación
multiplicacion=$((num1 * num2))
echo "Multiplicación: $num1 * $num2 = $multiplicacion"

# Bonus: División y módulo
division=$((num1 / num2))
modulo=$((num1 % num2))
echo ""
echo "=== Operaciones adicionales ==="
echo "División: $num1 / $num2 = $division"
echo "Módulo: $num1 % $num2 = $modulo"
```

Crear y ejecutar el script:
```bash
nano operaciones.sh
chmod +x operaciones.sh
./operaciones.sh
```

5. Crea un script que pida tu nombre con read y lo muestre.

```bash
#!/bin/bash
# Nombre: pedir_nombre.sh
# Descripción: Pide el nombre al usuario y lo muestra

# Pedir el nombre al usuario
echo "Por favor, introduce tu nombre:"
read nombre

# Mostrar el nombre
echo "Hola, $nombre! Bienvenido/a."

# Alternativa con prompt en la misma línea
# read -p "Introduce tu nombre: " nombre
# echo "Hola, $nombre!"

# Versión más completa
echo ""
echo "Encantado de conocerte, ${nombre}!"
```

Crear y ejecutar el script:
```bash
nano pedir_nombre.sh
chmod +x pedir_nombre.sh
./pedir_nombre.sh
```

6. Crea un script que pida dos números al usuario y muestre su suma.

```bash
#!/bin/bash
# Nombre: suma_numeros.sh
# Descripción: Pide dos números al usuario y muestra su suma

# Pedir el primer número
echo "Introduce el primer número:"
read num1

# Pedir el segundo número
echo "Introduce el segundo número:"
read num2

# Calcular la suma
suma=$((num1 + num2))

# Mostrar el resultado
echo ""
echo "La suma de $num1 + $num2 = $suma"

# Alternativa con read -p (prompt en la misma línea)
# read -p "Introduce el primer número: " num1
# read -p "Introduce el segundo número: " num2
# suma=$((num1 + num2))
# echo "La suma es: $suma"
```

Crear y ejecutar el script:
```bash
nano suma_numeros.sh
chmod +x suma_numeros.sh
./suma_numeros.sh
```

7. Crea un script con tres argumentos que muestre el primero y el tercero.

```bash
#!/bin/bash
# Nombre: argumentos_1_3.sh
# Descripción: Muestra el primer y tercer argumento

# Verificar que se pasaron al menos 3 argumentos
if [ $# -lt 3 ]; then
    echo "Error: Se necesitan 3 argumentos"
    echo "Uso: $0 argumento1 argumento2 argumento3"
    exit 1
fi

# Mostrar el primer y tercer argumento
echo "El primer argumento es: $1"
echo "El tercer argumento es: $3"

# Información adicional
echo ""
echo "=== Información adicional ==="
echo "El segundo argumento (no mostrado) es: $2"
echo "Total de argumentos recibidos: $#"
```

Crear y ejecutar el script:
```bash
nano argumentos_1_3.sh
chmod +x argumentos_1_3.sh
./argumentos_1_3.sh primero segundo tercero

# Ejemplo con diferentes valores
./argumentos_1_3.sh Hola Mundo Bash
```

8. Crea un script con argumentos que muestre el número total.

```bash
#!/bin/bash
# Nombre: contar_argumentos.sh
# Descripción: Muestra el número total de argumentos recibidos

# Mostrar el número total de argumentos
echo "Número total de argumentos: $#"

# Información adicional
if [ $# -eq 0 ]; then
    echo "No se recibieron argumentos"
elif [ $# -eq 1 ]; then
    echo "Se recibió 1 argumento: $1"
else
    echo "Se recibieron $# argumentos"
    echo "Todos los argumentos: $@"
fi

# Listar cada argumento
echo ""
echo "=== Lista de argumentos ==="
contador=1
for arg in "$@"; do
    echo "Argumento $contador: $arg"
    ((contador++))
done
```

Crear y ejecutar el script:
```bash
nano contar_argumentos.sh
chmod +x contar_argumentos.sh

# Probar con diferentes cantidades de argumentos
./contar_argumentos.sh
./contar_argumentos.sh uno
./contar_argumentos.sh uno dos tres
./contar_argumentos.sh Hola Mundo desde Bash
```

9. Crea un script que reciba dos números como argumentos y muestre su suma, resta, multiplicación y división.

```bash
#!/bin/bash
# Nombre: calculadora.sh
# Descripción: Realiza operaciones matemáticas con dos números como argumentos

# Verificar que se recibieron 2 argumentos
if [ $# -ne 2 ]; then
    echo "Error: Se necesitan exactamente 2 números"
    echo "Uso: $0 numero1 numero2"
    exit 1
fi

# Guardar los argumentos en variables
num1=$1
num2=$2

echo "=== CALCULADORA ==="
echo "Primer número: $num1"
echo "Segundo número: $num2"
echo ""

# Realizar las operaciones
suma=$((num1 + num2))
resta=$((num1 - num2))
multiplicacion=$((num1 * num2))

echo "Suma: $num1 + $num2 = $suma"
echo "Resta: $num1 - $num2 = $resta"
echo "Multiplicación: $num1 * $num2 = $multiplicacion"

# División (con verificación de división por cero)
if [ $num2 -eq 0 ]; then
    echo "División: No se puede dividir por cero"
else
    division=$((num1 / num2))
    modulo=$((num1 % num2))
    echo "División: $num1 / $num2 = $division"
    echo "Módulo: $num1 % $num2 = $modulo"
fi
```

Crear y ejecutar el script:
```bash
nano calculadora.sh
chmod +x calculadora.sh

# Probar con diferentes números
./calculadora.sh 20 5
./calculadora.sh 100 7
./calculadora.sh 15 0
```

10. Crea un script que cree un archivo de texto y guarde tu nombre en su interior.

```bash
#!/bin/bash
# Nombre: crear_archivo_nombre.sh
# Descripción: Crea un archivo de texto y guarda un nombre en él

# Definir el nombre del archivo
archivo="mi_nombre.txt"

# Definir el nombre a guardar
nombre="Juan Pérez"

# Crear el archivo y guardar el nombre
echo "$nombre" > "$archivo"

# Confirmar que se creó
echo "Archivo '$archivo' creado exitosamente"
echo "Contenido guardado: $nombre"

# Mostrar el contenido del archivo
echo ""
echo "=== Contenido del archivo ==="
cat "$archivo"

# Bonus: Añadir más información al archivo
echo "" >> "$archivo"
echo "Fecha de creación: $(date)" >> "$archivo"
echo "Directorio: $(pwd)" >> "$archivo"

echo ""
echo "=== Contenido completo del archivo ==="
cat "$archivo"
```

Crear y ejecutar el script:
```bash
nano crear_archivo_nombre.sh
chmod +x crear_archivo_nombre.sh
./crear_archivo_nombre.sh

# Verificar que se creó el archivo
ls -l mi_nombre.txt
cat mi_nombre.txt
```

Versión alternativa con input del usuario:
```bash
#!/bin/bash
# Nombre: crear_archivo_nombre_input.sh
# Descripción: Pide el nombre al usuario y lo guarda en un archivo

# Pedir el nombre al usuario
read -p "Introduce tu nombre: " nombre

# Definir el nombre del archivo
archivo="nombre_usuario.txt"

# Crear el archivo y guardar el nombre
echo "$nombre" > "$archivo"

echo "Tu nombre ha sido guardado en '$archivo'"
echo "Contenido: $(cat $archivo)"
```