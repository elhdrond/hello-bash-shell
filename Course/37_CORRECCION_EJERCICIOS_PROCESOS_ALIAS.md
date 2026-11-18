# PROCESOS Y ALIAS

## Posibles correcciones (ten en cuenta que pueden variar dependiendo de tu sistema operativo y directorios existentes)

1. Muestra todos los procesos del sistema.

```bash
# Mostrar todos los procesos con ps
ps aux

# Explicación de las opciones:
# a = mostrar procesos de todos los usuarios
# u = formato orientado al usuario (más información)
# x = incluir procesos sin terminal de control

# Alternativas:
ps -ef  # Formato estándar de System V

# En macOS también:
ps -A   # Todos los procesos

# Ver procesos en formato árbol (jerarquía)
ps auxf  # Linux
pstree   # Si está instalado

# Mostrar solo tus procesos
ps -u $USER

# Ver procesos con más detalles específicos
ps aux | grep nombre_proceso
```

2. Muestra el monitor interactivo de procesos.

```bash
# Monitor interactivo de procesos con top
top

# Una vez dentro de top:
# - Presiona 'q' para salir
# - Presiona 'h' para ayuda
# - Presiona 'k' para matar un proceso (te pedirá el PID)
# - Presiona 'M' para ordenar por uso de memoria
# - Presiona 'P' para ordenar por uso de CPU
# - Presiona 'u' para filtrar por usuario

# Alternativa moderna (más visual y amigable)
htop
# Nota: htop necesita instalarse primero
# macOS: brew install htop
# Linux: sudo apt-get install htop

# En htop:
# - F10 o 'q' para salir
# - F9 para matar un proceso
# - F6 para ordenar por columnas
# - Flechas para navegar
# - Más intuitivo y con colores

# Alternativa en macOS (monitor de actividad)
# También puedes abrir la aplicación gráfica:
open -a "Activity Monitor"
```

3. Utiliza el comando free de manera correcta.

```bash
# En Linux - Ver memoria RAM disponible
free

# Con formato más legible (KB, MB, GB)
free -h

# Mostrar en megabytes
free -m

# Mostrar en gigabytes
free -g

# Actualizar cada 2 segundos
free -h -s 2

# Mostrar totales
free -h -t

# IMPORTANTE: En macOS, el comando 'free' NO existe por defecto
# Alternativas en macOS:

# Ver estadísticas de memoria en macOS
vm_stat

# Comando más amigable en macOS
top -l 1 | head -n 10 | grep PhysMem

# O instalar una alternativa
# brew install freeutils
# Luego: freeutils free -h

# Ver memoria con sysctl (macOS)
sysctl -a | grep mem
```

4. Lanza sleep 100 en la terminal, suspéndelo, mándalo al segundo plano y tráelo al primer plano.

```bash
# Paso 1: Lanzar sleep 100
sleep 100

# Paso 2: Suspender el proceso (mientras está ejecutándose)
# Presiona: Ctrl + Z
# Verás algo como: [1]+ Stopped sleep 100

# Paso 3: Ver trabajos suspendidos
jobs
# Mostrará: [1]+ Stopped sleep 100

# Paso 4: Mandar al segundo plano (background)
bg %1
# O simplemente: bg
# Verás: [1]+ sleep 100 &
# Ahora el proceso continúa ejecutándose en segundo plano

# Verificar que está en background
jobs
# Mostrará: [1]+ Running sleep 100 &

# Paso 5: Traer al primer plano (foreground)
fg %1
# O simplemente: fg
# El proceso vuelve al primer plano

# Ahora puedes:
# - Ctrl + Z para suspenderlo de nuevo
# - Ctrl + C para terminarlo
# - Dejarlo correr hasta que termine

# Nota: También puedes lanzar directamente en background:
sleep 100 &
# El & al final lo ejecuta en segundo plano desde el inicio
```

5. Lanza un proceso como sleep y termínalo usando su PID.

```bash
# Paso 1: Lanzar sleep en segundo plano
sleep 200 &

# Esto mostrará algo como:
# [1] 12345
# Donde 12345 es el PID (Process ID)

# Paso 2: Si no guardaste el PID, búscalo
ps aux | grep sleep
# O más específico:
pgrep sleep

# También puedes usar:
jobs -l
# Mostrará: [1]+ 12345 Running sleep 200 &

# Paso 3: Terminar el proceso usando kill con el PID
kill 12345

# Verificar que se terminó
jobs
ps aux | grep sleep

# Otras señales de kill:
kill -9 12345    # SIGKILL - terminación forzada (no puede ser ignorada)
kill -15 12345   # SIGTERM - terminación normal (por defecto)
kill -TERM 12345 # Equivalente a -15
kill -KILL 12345 # Equivalente a -9

# Terminar por nombre del proceso (killall)
killall sleep

# En macOS/Linux modernos (pkill)
pkill sleep

# Ver todas las señales disponibles
kill -l
```

6. Consulta el espacio en disco.

```bash
# Ver espacio en disco de todos los sistemas de archivos
df

# Con formato legible (KB, MB, GB)
df -h

# Ver solo el sistema de archivos local (sin red)
df -hl

# Ver inodos en lugar de bloques
df -i

# Ver tipo de sistema de archivos
df -T  # Linux
df -h  # macOS muestra el tipo por defecto

# Ver espacio de un directorio específico
df -h /home
df -h .

# Ver uso de disco de directorios y archivos (disk usage)
du

# Tamaño de un directorio específico
du -sh /ruta/al/directorio

# Tamaño del directorio actual
du -sh .

# Ver tamaño de subdirectorios (profundidad 1)
du -h --max-depth=1  # Linux
du -hd 1             # macOS

# Top 10 directorios más grandes en el directorio actual
du -h | sort -hr | head -10

# Espacio usado y disponible resumido
df -h | grep -E "Filesystem|/$"
```

7. Consulta el historial.

```bash
# Ver todo el historial de comandos
history

# Ver los últimos 20 comandos
history 20

# Ver los últimos 10 comandos
history 10

# Buscar en el historial
history | grep "palabra_clave"

# Ejemplo: buscar todos los comandos con git
history | grep git

# Ejecutar un comando del historial por su número
!123  # Ejecuta el comando número 123

# Ejecutar el último comando que empieza con una palabra
!git  # Ejecuta el último comando que empezó con "git"

# Ver el archivo donde se guarda el historial
echo $HISTFILE
# Usualmente: ~/.bash_history o ~/.zsh_history

# Ver el contenido del archivo de historial directamente
cat ~/.bash_history  # Para bash
cat ~/.zsh_history   # Para zsh

# Limpiar el historial
history -c  # Limpia el historial en memoria
rm ~/.bash_history  # Elimina el archivo (requiere logout/login)

# Tamaño del historial
echo $HISTSIZE      # Número de comandos en memoria
echo $HISTFILESIZE  # Número de líneas en el archivo
```

8. Repite el último comando.

```bash
# Repetir el último comando
!!

# Ejemplo:
# ls -la
# !!    # Ejecuta de nuevo: ls -la

# Repetir el último comando con sudo
sudo !!

# Ejemplo útil:
# apt-get update
# Permission denied
# sudo !!  # Ejecuta: sudo apt-get update

# Repetir el penúltimo comando
!-2

# Repetir el último comando que empezó con una palabra
!ls   # Ejecuta el último comando que empezó con "ls"

# Usar el último argumento del comando anterior
cd /una/ruta/muy/larga
mkdir !$  # Crea directorio en /una/ruta/muy/larga

# Usar todos los argumentos del comando anterior
ls archivo1.txt archivo2.txt
cat !*  # Ejecuta: cat archivo1.txt archivo2.txt

# Reemplazar texto del último comando
^viejo^nuevo
# Ejemplo:
# cat archivo.tx
# ^tx^txt  # Ejecuta: cat archivo.txt

# Ver el último comando sin ejecutarlo
!ls:p  # Muestra el último comando "ls" sin ejecutarlo

# También puedes usar las flechas:
# ↑ (flecha arriba) para navegar por el historial
# ↓ (flecha abajo) para volver hacia adelante
```

9. Crea y prueba un alias.

```bash
# Crear un alias simple
alias ll='ls -la'

# Probar el alias
ll

# Crear más alias útiles
alias lh='ls -lh'                    # Listar con tamaños legibles
alias ..='cd ..'                     # Subir un nivel
alias ...='cd ../..'                 # Subir dos niveles
alias grep='grep --color=auto'       # grep con colores
alias la='ls -A'                     # Listar todo excepto . y ..
alias l='ls -CF'                     # Listar en columnas

# Alias con múltiples comandos
alias update='sudo apt-get update && sudo apt-get upgrade'  # Linux
alias cleanup='rm -rf *~ *.bak'      # Limpiar archivos temporales

# Alias con argumentos (usando funciones)
alias mkcd='function _mkcd(){ mkdir -p "$1" && cd "$1"; }; _mkcd'
# Uso: mkcd nueva_carpeta

# Ver todos los alias definidos
alias

# Ver un alias específico
alias ll

# Verificar si un comando es un alias
type ll
which ll

# Ignorar un alias temporalmente (usar el comando original)
\ls    # Ejecuta ls sin el alias

# Los alias creados así solo duran la sesión actual
# Para hacerlos permanentes, añádelos a:
# ~/.bashrc  (para bash)
# ~/.zshrc   (para zsh)

# Ejemplo de cómo añadirlo permanentemente:
echo "alias ll='ls -la'" >> ~/.bashrc
# o para zsh:
echo "alias ll='ls -la'" >> ~/.zshrc

# Recargar el archivo de configuración
source ~/.bashrc  # bash
source ~/.zshrc   # zsh
```

10. Elimina el alias que acabas de crear.

```bash
# Eliminar un alias específico
unalias ll

# Verificar que se eliminó
alias ll
# Mostrará: bash: alias: ll: not found

# O intentar usarlo
ll
# Mostrará: command not found: ll

# Eliminar múltiples alias
unalias ll lh la

# Eliminar todos los alias de la sesión actual
unalias -a

# Ver qué alias quedan
alias

# IMPORTANTE: unalias solo elimina el alias de la sesión actual
# Si lo añadiste a ~/.bashrc o ~/.zshrc, seguirá apareciendo
# en nuevas sesiones

# Para eliminarlo permanentemente:
# 1. Editar el archivo de configuración
nano ~/.bashrc   # o ~/.zshrc

# 2. Buscar y eliminar la línea del alias
# Por ejemplo, eliminar: alias ll='ls -la'

# 3. Guardar y salir (Ctrl + O, Enter, Ctrl + X en nano)

# 4. Recargar la configuración
source ~/.bashrc  # o source ~/.zshrc

# Alternativa: eliminar con sed (sin abrir editor)
sed -i.bak '/alias ll=/d' ~/.bashrc  # Linux
sed -i '' '/alias ll=/d' ~/.bashrc   # macOS

# Ver el contenido del archivo para verificar
grep "alias ll" ~/.bashrc
# No debería mostrar nada si se eliminó correctamente
```