# LÓGICA

## Posibles correcciones (ten en cuenta que pueden variar dependiendo de tu sistema operativo y directorios existentes)

1. Crea un script que pida un número y muestre si es positivo, negativo o cero usando if, elif y else.

```bash
#!/bin/bash
# Nombre: positivo_negativo.sh
# Descripción: Verifica si un número es positivo, negativo o cero

# Pedir un número al usuario
read -p "Introduce un número: " numero

# Verificar si es positivo, negativo o cero
if [ $numero -gt 0 ]; then
    echo "El número $numero es positivo"
elif [ $numero -lt 0 ]; then
    echo "El número $numero es negativo"
else
    echo "El número es cero"
fi
```

Crear y ejecutar el script:
```bash
nano positivo_negativo.sh
chmod +x positivo_negativo.sh
./positivo_negativo.sh
```

2. Pide al usuario dos números y muestra cuál es mayor o si son iguales.

```bash
#!/bin/bash
# Nombre: comparar_numeros.sh
# Descripción: Compara dos números y muestra cuál es mayor

# Pedir dos números al usuario
read -p "Introduce el primer número: " num1
read -p "Introduce el segundo número: " num2

# Comparar los números
if [ $num1 -gt $num2 ]; then
    echo "El número $num1 es mayor que $num2"
elif [ $num1 -lt $num2 ]; then
    echo "El número $num2 es mayor que $num1"
else
    echo "Los números son iguales: $num1 = $num2"
fi
```

Crear y ejecutar el script:
```bash
nano comparar_numeros.sh
chmod +x comparar_numeros.sh
./comparar_numeros.sh
```

3. Crea un script que muestre un menú con tres opciones y ejecute la opción correspondiente según la elección del usuario.

```bash
#!/bin/bash
# Nombre: menu.sh
# Descripción: Muestra un menú con tres opciones

# Mostrar el menú
echo "=== MENÚ PRINCIPAL ==="
echo "1. Mostrar fecha y hora"
echo "2. Listar archivos del directorio"
echo "3. Mostrar información del usuario"
echo "======================="
read -p "Elige una opción (1-3): " opcion

# Ejecutar la opción elegida
case $opcion in
    1)
        echo ""
        echo "Fecha y hora actual:"
        date
        ;;
    2)
        echo ""
        echo "Archivos en el directorio actual:"
        ls -lh
        ;;
    3)
        echo ""
        echo "Información del usuario:"
        echo "Usuario: $USER"
        echo "Directorio home: $HOME"
        echo "Shell actual: $SHELL"
        ;;
    *)
        echo "Opción inválida. Por favor, elige 1, 2 o 3."
        ;;
esac
```

Crear y ejecutar el script:
```bash
nano menu.sh
chmod +x menu.sh
./menu.sh
```

4. Muestra todos los números del 1 al 10 usando un bucle for.

```bash
#!/bin/bash
# Nombre: bucle_for_1_10.sh
# Descripción: Muestra los números del 1 al 10 con bucle for

echo "Números del 1 al 10:"

# Bucle for con secuencia
for i in {1..10}
do
    echo $i
done

# Alternativa 1: usando seq
echo ""
echo "=== Alternativa con seq ==="
for i in $(seq 1 10)
do
    echo $i
done

# Alternativa 2: estilo C
echo ""
echo "=== Alternativa estilo C ==="
for ((i=1; i<=10; i++))
do
    echo $i
done
```

Crear y ejecutar el script:
```bash
nano bucle_for_1_10.sh
chmod +x bucle_for_1_10.sh
./bucle_for_1_10.sh
```

5. Crea un script que pida números al usuario hasta que introduzca el número 0. Al final, muestra cuántos números ha introducido en total.

```bash
#!/bin/bash
# Nombre: contar_numeros.sh
# Descripción: Pide números hasta que el usuario introduzca 0

# Inicializar contador
contador=0

echo "Introduce números (0 para terminar):"

# Bucle while infinito
while true
do
    read -p "Número: " numero
    
    # Verificar si es 0 para salir
    if [ $numero -eq 0 ]; then
        break
    fi
    
    # Incrementar contador
    ((contador++))
done

# Mostrar el resultado
echo ""
echo "Has introducido $contador números en total."
```

Versión alternativa:
```bash
#!/bin/bash

contador=0
numero=1  # Inicializar con valor diferente de 0

echo "Introduce números (0 para terminar):"

while [ $numero -ne 0 ]
do
    read -p "Número: " numero
    
    if [ $numero -ne 0 ]; then
        ((contador++))
    fi
done

echo "Has introducido $contador números en total."
```

Crear y ejecutar el script:
```bash
nano contar_numeros.sh
chmod +x contar_numeros.sh
./contar_numeros.sh
```

6. Haz un script que muestre los números del 1 al 10, saltando el 5 y deteniéndose en el 8.

```bash
#!/bin/bash
# Nombre: continue_break.sh
# Descripción: Muestra números del 1 al 10, salta el 5 y se detiene en el 8

echo "Números del 1 al 10 (saltando el 5 y deteniéndose en el 8):"

for i in {1..10}
do
    # Saltar el número 5
    if [ $i -eq 5 ]; then
        continue
    fi
    
    # Mostrar el número
    echo $i
    
    # Detenerse después del 8
    if [ $i -eq 8 ]; then
        break
    fi
done

echo "Bucle terminado."
```

Versión con más explicación:
```bash
#!/bin/bash
# continue_break_explicado.sh

echo "=== Bucle con continue y break ==="
echo "Saltaremos el 5 (continue) y nos detendremos en el 8 (break)"
echo ""

for i in {1..10}
do
    # continue: salta a la siguiente iteración
    if [ $i -eq 5 ]; then
        echo "[Saltando el $i]"
        continue
    fi
    
    echo "Número: $i"
    
    # break: sale del bucle completamente
    if [ $i -eq 8 ]; then
        echo "[Deteniéndose en el $i]"
        break
    fi
done

echo ""
echo "Fin del bucle."
```

Crear y ejecutar el script:
```bash
nano continue_break.sh
chmod +x continue_break.sh
./continue_break.sh
```

7. Crea una función saludar que reciba un nombre como argumento y muestre: Hola <nombre>, bienvenido al script.

```bash
#!/bin/bash
# Nombre: funcion_saludar.sh
# Descripción: Función que saluda con el nombre proporcionado

# Definir la función
saludar() {
    nombre=$1
    echo "Hola $nombre, bienvenido al script."
}

# Llamar a la función con diferentes nombres
saludar "Juan"
saludar "María"
saludar "Pedro"

# Pedir nombre al usuario y saludar
echo ""
read -p "Introduce tu nombre: " mi_nombre
saludar "$mi_nombre"
```

Versión con validación:
```bash
#!/bin/bash
# funcion_saludar_validacion.sh

# Función con validación
saludar() {
    if [ -z "$1" ]; then
        echo "Error: No se proporcionó un nombre"
        return 1
    fi
    
    nombre=$1
    echo "Hola $nombre, bienvenido al script."
}

# Probar la función
saludar "Ana"
saludar ""  # Sin argumento
saludar "Carlos"
```

Crear y ejecutar el script:
```bash
nano funcion_saludar.sh
chmod +x funcion_saludar.sh
./funcion_saludar.sh
```

8. Crea una función que reciba dos números, calcule su suma y la devuelva usando return. Muestra el resultado en el script principal.

```bash
#!/bin/bash
# Nombre: funcion_suma.sh
# Descripción: Función que suma dos números y devuelve el resultado

# Función para sumar
sumar() {
    local num1=$1
    local num2=$2
    local suma=$((num1 + num2))
    
    # return solo puede devolver valores entre 0-255
    # Por eso usamos echo para devolver el resultado
    echo $suma
}

# Llamar a la función y capturar el resultado
resultado=$(sumar 5 3)
echo "La suma de 5 + 3 = $resultado"

resultado=$(sumar 10 20)
echo "La suma de 10 + 20 = $resultado"

# Pedir números al usuario
read -p "Introduce el primer número: " a
read -p "Introduce el segundo número: " b
resultado=$(sumar $a $b)
echo "La suma de $a + $b = $resultado"
```

Versión alternativa usando variable global:
```bash
#!/bin/bash
# funcion_suma_return.sh

# Nota: return en bash solo devuelve códigos de estado (0-255)
# Para devolver valores, usamos variables globales o echo

# Versión con variable global
sumar_global() {
    local num1=$1
    local num2=$2
    RESULTADO=$((num1 + num2))
}

echo "=== Usando variable global ==="
sumar_global 15 25
echo "Resultado: $RESULTADO"

# Versión con echo (recomendada)
sumar_echo() {
    local num1=$1
    local num2=$2
    echo $((num1 + num2))
}

echo ""
echo "=== Usando echo (capturando con \$()) ==="
resultado=$(sumar_echo 7 8)
echo "Resultado: $resultado"
```

Crear y ejecutar el script:
```bash
nano funcion_suma.sh
chmod +x funcion_suma.sh
./funcion_suma.sh
```

9. Intenta copiar un archivo que no exista y muestra un mensaje de error si el comando falla, usando $? o ||.

```bash
#!/bin/bash
# Nombre: manejo_errores.sh
# Descripción: Manejo de errores al copiar archivos

echo "=== Método 1: Usando \$? ==="
# Intentar copiar un archivo que no existe
cp archivo_que_no_existe.txt destino.txt

# Verificar el código de salida
if [ $? -ne 0 ]; then
    echo "Error: No se pudo copiar el archivo"
else
    echo "Archivo copiado exitosamente"
fi

echo ""
echo "=== Método 2: Usando || (OR) ==="
# Si el comando falla (retorna no-cero), ejecuta lo que está después de ||
cp otro_archivo_inexistente.txt destino2.txt || echo "Error: El archivo no existe"

echo ""
echo "=== Método 3: Usando && (AND) ==="
# Si el comando tiene éxito (retorna 0), ejecuta lo que está después de &&
cp archivo_real.txt copia.txt && echo "Archivo copiado con éxito" || echo "Error al copiar"

echo ""
echo "=== Método 4: Manejo completo ==="
archivo_origen="archivo_inexistente.txt"
archivo_destino="destino.txt"

if [ ! -f "$archivo_origen" ]; then
    echo "Error: El archivo '$archivo_origen' no existe"
    exit 1
fi

cp "$archivo_origen" "$archivo_destino"
if [ $? -eq 0 ]; then
    echo "Archivo copiado exitosamente"
else
    echo "Error al copiar el archivo"
fi
```

Versión simplificada:
```bash
#!/bin/bash
# manejo_errores_simple.sh

echo "Intentando copiar un archivo que no existe..."

# Usando ||
cp archivo_inexistente.txt destino.txt || {
    echo "Error: No se pudo copiar el archivo"
    echo "El archivo probablemente no existe"
}

echo ""
echo "Script finalizado."
```

Crear y ejecutar el script:
```bash
nano manejo_errores.sh
chmod +x manejo_errores.sh
./manejo_errores.sh
```

10. Crea un script con un comentario inicial con autor, fecha, descripción y un bucle for que liste todos los archivos .sh en el directorio actual.

```bash
#!/bin/bash
# Nombre: listar_scripts.sh
# Descripción: Este script lista todos los archivos con extensión .sh que se encuentran en el directorio actual.

echo "=== Listado de archivos .sh en el directorio actual ==="
echo "Directorio: $(pwd)"
echo ""

# Contador de archivos
contador=0

# Bucle for para listar archivos .sh
for archivo in *.sh
do
    # Verificar si existen archivos .sh
    if [ -e "$archivo" ]; then
        ((contador++))
        echo "$contador. $archivo"
        
        # Información adicional del archivo
        tamanio=$(ls -lh "$archivo" | awk '{print $5}')
        echo "   Tamaño: $tamanio"
        
        # Verificar si tiene permisos de ejecución
        if [ -x "$archivo" ]; then
            echo "   Permisos: Ejecutable ✓"
        else
            echo "   Permisos: No ejecutable"
        fi
        echo ""
    else
        echo "No se encontraron archivos .sh en este directorio"
        break
    fi
done

# Resumen
if [ $contador -gt 0 ]; then
    echo "Total de archivos .sh encontrados: $contador"
else
    echo "Total de archivos .sh encontrados: 0"
fi

echo ""
echo "Fecha de ejecución: $(date '+%d/%m/%Y %H:%M:%S')"
```

Versión simplificada:
```bash
#!/bin/bash
# Script: listar_scripts_simple.sh
# Descripción: Lista archivos .sh en el directorio actual

echo "Archivos .sh en el directorio actual:"
echo ""

for archivo in *.sh
do
    if [ -f "$archivo" ]; then
        echo "- $archivo"
    fi
done
```

Crear y ejecutar el script:
```bash
nano listar_scripts.sh
chmod +x listar_scripts.sh
./listar_scripts.sh
```