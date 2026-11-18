# GESTIÓN DE ARCHIVOS

## Posibles correcciones (ten en cuenta que pueden variar dependiendo de tu sistema operativo y directorios existentes)

1. Crea un directorio.

```bash
mkdir mi_directorio
# O con la opción -p para crear directorios anidados
mkdir -p directorio_padre/directorio_hijo
```

2. Elimina el directorio que acabas de crear.

```bash
rmdir mi_directorio
# Para eliminar directorios anidados vacíos
rmdir directorio_padre/directorio_hijo
rmdir directorio_padre
```

3. Copia un archivo en el directorio actual y fuera de éste.

```bash
# Copiar un archivo en el directorio actual con otro nombre
cp archivo.txt archivo_copia.txt

# Copiar un archivo a otro directorio
cp archivo.txt /ruta/al/otro/directorio/

# Copiar un archivo desde otro directorio al actual
cp /ruta/al/archivo.txt .
```

4. Mueve un archivo del directorio actual.

```bash
# Mover un archivo a otro directorio
mv archivo.txt /ruta/al/directorio_destino/

# Mover un archivo al directorio padre
mv archivo.txt ..

# Mover un archivo a un subdirectorio
mv archivo.txt subdirectorio/
```

5. Cambia el nombre del archivo que acabas de mover.

```bash
# Renombrar un archivo (mv también sirve para renombrar)
mv subdirectorio/archivo.txt subdirectorio/archivo_renombrado.txt

# O si estás en el directorio donde está el archivo
cd subdirectorio
mv archivo.txt nuevo_nombre.txt
```

6. Lista todos los archivos de un tipo usando un comodín.

```bash
# Listar todos los archivos .txt
ls *.txt

# Listar todos los archivos .sh
ls *.sh

# Listar todos los archivos .md
ls *.md

# Listar con detalles
ls -l *.txt

# Listar recursivamente todos los archivos de un tipo
ls -R *.txt
```

7. Elimina un directorio de manera recursiva (cuidado con lo que vas a borrar).

```bash
# Eliminar un directorio y todo su contenido de forma recursiva
rm -r nombre_directorio

# Con confirmación antes de eliminar
rm -ri nombre_directorio

# Forzar eliminación sin confirmación (¡CUIDADO!)
rm -rf nombre_directorio

# Forma más segura con verbose para ver qué se elimina
rm -rv nombre_directorio
```

8. Elimina todos los archivos de un mismo tipo (cuidado con lo que vas a borrar).

```bash
# Eliminar todos los archivos .txt del directorio actual
rm *.txt

# Con confirmación para cada archivo
rm -i *.txt

# Eliminar archivos de un tipo específico con verbose
rm -v *.log

# Eliminar archivos de varios tipos
rm *.txt *.log *.tmp

# Eliminar recursivamente todos los archivos de un tipo en subdirectorios
find . -name "*.txt" -type f -delete
```

9. Utiliza el comando tree.

```bash
# Mostrar árbol de directorios del directorio actual
tree

# Mostrar árbol con un nivel de profundidad específico
tree -L 2

# Mostrar solo directorios
tree -d

# Mostrar con tamaños de archivo
tree -h

# Mostrar solo archivos de un tipo específico
tree -P "*.txt"

# Mostrar árbol con todos los detalles
tree -a -h -L 3

# Si no tienes tree instalado, puedes instalarlo:
# En macOS: brew install tree
# En Linux: sudo apt-get install tree (Debian/Ubuntu)
#           sudo yum install tree (RedHat/CentOS)
```

10. Busca un archivo concreto en el directorio actual utilizando find.

```bash
# Buscar un archivo específico por nombre en el directorio actual
find . -name "archivo.txt"

# Buscar sin distinguir mayúsculas/minúsculas
find . -iname "archivo.txt"

# Buscar todos los archivos con una extensión específica
find . -name "*.sh"

# Buscar solo archivos (no directorios)
find . -type f -name "archivo.txt"

# Buscar solo directorios
find . -type d -name "mi_directorio"

# Buscar archivos modificados en las últimas 24 horas
find . -type f -mtime -1

# Buscar archivos y mostrar detalles
find . -name "*.md" -ls

# Buscar y ejecutar un comando en cada resultado
find . -name "*.txt" -exec ls -lh {} \;

# Buscar archivos por tamaño (mayores de 1MB)
find . -type f -size +1M
```