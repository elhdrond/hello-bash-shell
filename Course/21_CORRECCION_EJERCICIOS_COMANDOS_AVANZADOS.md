# COMANDOS AVANZADOS

## Posibles correcciones (ten en cuenta que pueden variar dependiendo de tu sistema operativo y directorios existentes)

1. Muestra todo el contenido de un archivo.

```bash
# Mostrar todo el contenido de un archivo
cat archivo.txt

# Mostrar con números de línea
cat -n archivo.txt

# Mostrar múltiples archivos
cat archivo1.txt archivo2.txt
```

2. Muestra el contenido paginado de un archivo.

```bash
# Mostrar contenido paginado con less (más moderno y recomendado)
less archivo.txt

# Mostrar contenido paginado con more (tradicional)
more archivo.txt

# Con less puedes:
# - Usar las flechas o j/k para navegar
# - Presionar 'q' para salir
# - Buscar con '/' seguido del término
# - Usar 'n' para siguiente resultado y 'N' para anterior
```

3. Muestra las 15 primeras líneas de un archivo.

```bash
# Mostrar las 15 primeras líneas
head -n 15 archivo.txt

# O simplemente (alternativa)
head -15 archivo.txt

# Por defecto head muestra 10 líneas
head archivo.txt
```

4. Muestra las 15 últimas líneas de un archivo.

```bash
# Mostrar las 15 últimas líneas
tail -n 15 archivo.txt

# O simplemente (alternativa)
tail -15 archivo.txt

# Por defecto tail muestra 10 líneas
tail archivo.txt

# Seguir mostrando nuevas líneas en tiempo real (útil para logs)
tail -f archivo.log
```

5. Busca una palabra en un archivo.

```bash
# Buscar una palabra en un archivo con grep
grep "palabra" archivo.txt

# Buscar sin distinguir mayúsculas/minúsculas
grep -i "palabra" archivo.txt

# Mostrar número de línea donde aparece
grep -n "palabra" archivo.txt

# Buscar en múltiples archivos
grep "palabra" *.txt

# Buscar recursivamente en directorios
grep -r "palabra" .

# Buscar la línea completa que contiene la palabra
grep -w "palabra" archivo.txt

# Contar cuántas veces aparece
grep -c "palabra" archivo.txt
```

6. Cuenta las líneas de un archivo.

```bash
# Contar líneas de un archivo con wc (word count)
wc -l archivo.txt

# Mostrar líneas, palabras y caracteres
wc archivo.txt

# Solo palabras
wc -w archivo.txt

# Solo caracteres
wc -c archivo.txt

# Contar líneas de múltiples archivos
wc -l *.txt
```

7. Redirige una salida y guárdala en un archivo.

```bash
# Redirigir salida estándar a un archivo (sobrescribe)
ls -l > listado.txt

# Redirigir salida de cualquier comando
echo "Hola mundo" > saludo.txt

# Redirigir salida de error
comando_que_falla 2> errores.txt

# Redirigir tanto salida estándar como error al mismo archivo
comando > salida.txt 2>&1

# Forma moderna (bash 4+)
comando &> salida.txt

# Descartar salida (enviar a /dev/null)
comando > /dev/null
```

8. Añade una nueva salida al archivo anterior.

```bash
# Añadir (append) salida al final de un archivo existente con >>
echo "Nueva línea" >> saludo.txt

# Añadir resultado de un comando
date >> saludo.txt

# Añadir listado al archivo anterior
ls -l >> listado.txt

# Añadir errores al archivo de errores
comando_que_falla 2>> errores.txt

# Añadir tanto salida estándar como error
comando >> salida.txt 2>&1
```

9. Encadena 3 comandos.

```bash
# Encadenar con pipe (|) - la salida de uno es entrada del siguiente
ls -l | grep "txt" | wc -l

# Otro ejemplo: listar, filtrar y ordenar
cat archivo.txt | grep "error" | sort

# Ejemplo más complejo: buscar, contar y guardar
find . -name "*.sh" | wc -l | tee resultado.txt

# Encadenar con AND (&&) - ejecuta el siguiente solo si el anterior tuvo éxito
mkdir nuevo_dir && cd nuevo_dir && touch archivo.txt

# Encadenar con OR (||) - ejecuta el siguiente solo si el anterior falló
comando1 || comando2 || comando3

# Encadenar con punto y coma (;) - ejecuta todos sin importar el resultado
echo "Primero" ; echo "Segundo" ; echo "Tercero"
```

10. Crea una variable local y muéstrala.

```bash
# Crear una variable local (sin espacios alrededor del =)
nombre="Juan"

# Mostrar el valor de la variable con echo
echo $nombre

# Mostrar con llaves (recomendado)
echo ${nombre}

# Crear variable numérica
edad=25
echo $edad

# Crear variable con resultado de comando
fecha=$(date)
echo $fecha

# Alternativa con backticks (antigua)
fecha=`date`
echo $fecha

# Mostrar con texto
echo "Mi nombre es $nombre y tengo $edad años"

# Ver todas las variables
set

# Ver solo variables de entorno
env
```