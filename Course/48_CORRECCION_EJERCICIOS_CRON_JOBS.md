# CRON JOBS

## Posibles correcciones (ten en cuenta que pueden variar dependiendo de tu sistema operativo y directorios existentes)

1. Crea un script que muestre la fecha y hora actual en un archivo. Programa su ejecución cada minuto con una cron.

```bash
#!/bin/bash
# Nombre: fecha_hora.sh
# Descripción: Guarda la fecha y hora actual en un archivo

# Definir el archivo de salida
archivo="$HOME/fecha_hora.log"

# Escribir la fecha y hora en el archivo
echo "Fecha y hora: $(date '+%d/%m/%Y %H:%M:%S')" >> "$archivo"
```

Pasos para configurar:
```bash
# 1. Crear el script
nano ~/fecha_hora.sh

# 2. Dar permisos de ejecución
chmod +x ~/fecha_hora.sh

# 3. Probar el script
~/fecha_hora.sh
cat ~/fecha_hora.log

# 4. Editar crontab
crontab -e

# 5. Añadir esta línea al crontab:
* * * * * $HOME/fecha_hora.sh

# 6. Verificar que se añadió correctamente
crontab -l

# 7. Esperar 1-2 minutos y verificar el archivo
tail -f ~/fecha_hora.log
```

Explicación del cron:
```
* * * * * comando
│ │ │ │ │
│ │ │ │ └─── Día de la semana (0-7, donde 0 y 7 = domingo)
│ │ │ └───── Mes (1-12)
│ │ └─────── Día del mes (1-31)
│ └───────── Hora (0-23)
└─────────── Minuto (0-59)

* = cada minuto/hora/día/mes/día de semana
```

2. Crea un script que muestre "Hola desde cron" en un archivo. Configura cron para ejecutarlo cada 5 minutos.

```bash
#!/bin/bash
# Nombre: hola_cron.sh
# Descripción: Escribe un mensaje en un archivo cada 5 minutos

# Archivo de salida
archivo="$HOME/hola_cron.log"

# Escribir mensaje con fecha
echo "[$(date '+%Y-%m-%d %H:%M:%S')] Hola desde cron" >> "$archivo"
```

Configurar crontab:
```bash
# 1. Crear y preparar el script
nano ~/hola_cron.sh
chmod +x ~/hola_cron.sh

# 2. Editar crontab
crontab -e

# 3. Añadir esta línea (ejecutar cada 5 minutos):
*/5 * * * * $HOME/hola_cron.sh

# 4. Verificar
crontab -l

# 5. Monitorear el archivo
tail -f ~/hola_cron.log
```

Explicación:
```
*/5 * * * * = Cada 5 minutos
*/10 * * * * = Cada 10 minutos
*/15 * * * * = Cada 15 minutos
*/30 * * * * = Cada 30 minutos
```

3. Escribe un script de backup que comprima una carpeta en un archivo con fecha. Programa su ejecución cada día a las 2:00 AM.

```bash
#!/bin/bash
# Nombre: backup_diario.sh
# Descripción: Realiza backup comprimido de una carpeta

# Configuración
carpeta_origen="$HOME/documentos"
carpeta_destino="$HOME/backups"
fecha=$(date '+%Y%m%d_%H%M%S')
nombre_backup="backup_${fecha}.tar.gz"

# Crear carpeta de destino si no existe
mkdir -p "$carpeta_destino"

# Realizar backup
tar -czf "$carpeta_destino/$nombre_backup" -C "$HOME" "documentos" 2>/dev/null

# Registrar en log
log_file="$HOME/backups/backup.log"
if [ $? -eq 0 ]; then
    echo "[$(date '+%Y-%m-%d %H:%M:%S')] Backup exitoso: $nombre_backup" >> "$log_file"
else
    echo "[$(date '+%Y-%m-%d %H:%M:%S')] Error en backup" >> "$log_file"
fi

# Opcional: Eliminar backups antiguos (más de 7 días)
find "$carpeta_destino" -name "backup_*.tar.gz" -mtime +7 -delete
```

Configurar crontab:
```bash
# 1. Crear el script
nano ~/backup_diario.sh
chmod +x ~/backup_diario.sh

# 2. Crear carpetas necesarias
mkdir -p ~/documentos ~/backups

# 3. Probar el script manualmente
~/backup_diario.sh
ls -lh ~/backups/

# 4. Editar crontab
crontab -e

# 5. Añadir para ejecutar a las 2:00 AM diariamente:
0 2 * * * $HOME/backup_diario.sh

# 6. Verificar
crontab -l
```

Explicación del cron:
```
0 2 * * * = A las 2:00 AM todos los días
30 3 * * * = A las 3:30 AM todos los días
0 0 * * * = A medianoche (00:00) todos los días
```

4. Haz un script que borre archivos .log de una carpeta temporal. Programa su ejecución todos los domingos a la medianoche.

```bash
#!/bin/bash
# Nombre: limpiar_logs.sh
# Descripción: Elimina archivos .log de carpeta temporal

# Carpeta a limpiar
carpeta_temporal="$HOME/temp_logs"

# Archivo de registro
log_limpieza="$HOME/limpieza.log"

# Crear carpeta si no existe
mkdir -p "$carpeta_temporal"

# Contar archivos antes de eliminar
cantidad_antes=$(find "$carpeta_temporal" -name "*.log" -type f | wc -l)

# Eliminar archivos .log
find "$carpeta_temporal" -name "*.log" -type f -delete

# Contar archivos después
cantidad_despues=$(find "$carpeta_temporal" -name "*.log" -type f | wc -l)
eliminados=$((cantidad_antes - cantidad_despues))

# Registrar la acción
echo "[$(date '+%Y-%m-%d %H:%M:%S')] Archivos .log eliminados: $eliminados" >> "$log_limpieza"
```

Configurar crontab:
```bash
# 1. Crear el script
nano ~/limpiar_logs.sh
chmod +x ~/limpiar_logs.sh

# 2. Crear carpeta temporal y algunos archivos de prueba
mkdir -p ~/temp_logs
touch ~/temp_logs/test{1..5}.log

# 3. Probar el script
~/limpiar_logs.sh
cat ~/limpieza.log

# 4. Editar crontab
crontab -e

# 5. Añadir para ejecutar domingos a medianoche:
0 0 * * 0 $HOME/limpiar_logs.sh

# 6. Verificar
crontab -l
```

Explicación días de la semana:
```
0 0 * * 0 = Domingo a medianoche
0 0 * * 1 = Lunes a medianoche
0 0 * * 6 = Sábado a medianoche
0 0 * * 1-5 = Lunes a viernes a medianoche
0 0 * * 0,6 = Fines de semana a medianoche

Días: 0 o 7 = Domingo, 1 = Lunes, 2 = Martes, ..., 6 = Sábado
```

5. Programa un script que escriba la hora actual, ejecutándose cada hora de 9 a 17 (horario laboral).

```bash
#!/bin/bash
# Nombre: horario_laboral.sh
# Descripción: Registra la hora durante el horario laboral

# Archivo de salida
archivo="$HOME/horario_laboral.log"

# Escribir hora actual
echo "Hora registrada: $(date '+%H:%M:%S - %d/%m/%Y')" >> "$archivo"
```

Configurar crontab:
```bash
# 1. Crear el script
nano ~/horario_laboral.sh
chmod +x ~/horario_laboral.sh

# 2. Probar
~/horario_laboral.sh
cat ~/horario_laboral.log

# 3. Editar crontab
crontab -e

# 4. Añadir para ejecutar cada hora de 9 AM a 5 PM:
0 9-17 * * * $HOME/horario_laboral.sh

# O si quieres incluir también la 6 PM (hasta las 17:00, no incluye 18:00):
# 0 9-17 * * * $HOME/horario_laboral.sh

# 5. Verificar
crontab -l
```

Explicación de rangos de hora:
```
0 9-17 * * * = Cada hora de 9:00 a 17:00
0 9-17 * * 1-5 = Cada hora de 9 a 17, solo lunes a viernes
30 9-17 * * * = A los 30 minutos de cada hora (9:30, 10:30, etc.)
0 8-18/2 * * * = Cada 2 horas de 8:00 a 18:00 (8, 10, 12, 14, 16, 18)
0 9,12,15,17 * * * = A las 9, 12, 15 y 17 horas
```

6. Programa un script que muestre "Hoy toca practicar" en un archivo de log solo los lunes, miércoles y viernes a las 8:00 AM.

```bash
#!/bin/bash
# Nombre: practicar.sh
# Descripción: Recordatorio para practicar lunes, miércoles y viernes

# Archivo de log
archivo="$HOME/recordatorios.log"

# Obtener el día de la semana
dia_semana=$(date '+%A')

# Escribir mensaje
echo "[$(date '+%Y-%m-%d %H:%M:%S')] - $dia_semana - Hoy toca practicar" >> "$archivo"
```

Configurar crontab:
```bash
# 1. Crear el script
nano ~/practicar.sh
chmod +x ~/practicar.sh

# 2. Probar
~/practicar.sh
cat ~/recordatorios.log

# 3. Editar crontab
crontab -e

# 4. Añadir para lunes (1), miércoles (3) y viernes (5) a las 8:00 AM:
0 8 * * 1,3,5 $HOME/practicar.sh

# 5. Verificar
crontab -l
```

Explicación de múltiples días:
```
0 8 * * 1,3,5 = Lunes, miércoles y viernes a las 8:00 AM
0 8 * * 1-5 = Lunes a viernes (toda la semana laboral) a las 8:00 AM
0 8 * * 0,6 = Sábado y domingo a las 8:00 AM
0 8 * * 2,4 = Martes y jueves a las 8:00 AM
30 14 * * 1,3,5 = Lunes, miércoles y viernes a las 14:30
```

7. Modifica uno de los scripts para que su salida y errores se guarden en cron.log.

```bash
#!/bin/bash
# Nombre: fecha_hora_logs.sh
# Descripción: Guarda fecha/hora con manejo de salida y errores

archivo="$HOME/fecha_hora_output.log"

# Simulando algunas operaciones que podrían generar salida y errores
echo "=== Inicio de ejecución ===" 
echo "Fecha y hora: $(date '+%d/%m/%Y %H:%M:%S')" >> "$archivo"

# Verificar si el archivo se creó correctamente
if [ $? -eq 0 ]; then
    echo "Registro exitoso"
else
    echo "Error al escribir en el archivo" >&2
fi
```

Configurar crontab con redirección:
```bash
# 1. Crear el script
nano ~/fecha_hora_logs.sh
chmod +x ~/fecha_hora_logs.sh

# 2. Editar crontab
crontab -e

# 3. OPCIÓN 1: Redirigir salida estándar y errores al mismo archivo
* * * * * $HOME/fecha_hora_logs.sh >> $HOME/cron.log 2>&1

# 4. OPCIÓN 2: Redirigir a archivos separados
* * * * * $HOME/fecha_hora_logs.sh >> $HOME/cron_output.log 2>> $HOME/cron_error.log

# 5. OPCIÓN 3: Solo errores a archivo, salida descartada
* * * * * $HOME/fecha_hora_logs.sh > /dev/null 2>> $HOME/cron.log

# 6. Verificar
crontab -l

# 7. Ver los logs
tail -f ~/cron.log
```

Explicación de redirecciones:
```bash
comando >> archivo.log 2>&1
# >> = Añadir salida estándar al archivo
# 2>&1 = Redirigir errores (2) a donde va salida estándar (1)

comando > salida.log 2> error.log
# > = Sobrescribir salida estándar
# 2> = Sobrescribir errores

comando &>> archivo.log
# &>> = Añadir tanto salida como errores (bash 4+)

comando > /dev/null 2>&1
# Descartar toda salida y errores
```

8. Programa un script que muestre "Sistema OK" y lo ejecute cada 10 minutos.

```bash
#!/bin/bash
# Nombre: sistema_ok.sh
# Descripción: Monitoreo simple del sistema

# Archivo de log
log_file="$HOME/sistema_monitor.log"

# Obtener información del sistema
carga=$(uptime | awk -F'load average:' '{print $2}' | awk '{print $1}')
memoria_libre=$(free -h 2>/dev/null | grep Mem | awk '{print $4}' || echo "N/A")

# Escribir estado
echo "[$(date '+%Y-%m-%d %H:%M:%S')] Sistema OK - Carga: $carga - Memoria libre: $memoria_libre" >> "$log_file"
```

Versión simplificada:
```bash
#!/bin/bash
# sistema_ok_simple.sh

archivo="$HOME/sistema_ok.log"
echo "[$(date '+%Y-%m-%d %H:%M:%S')] Sistema OK" >> "$archivo"
```

Configurar crontab:
```bash
# 1. Crear el script (versión simple)
nano ~/sistema_ok.sh
chmod +x ~/sistema_ok.sh

# 2. Probar
~/sistema_ok.sh
cat ~/sistema_ok.log

# 3. Editar crontab
crontab -e

# 4. Añadir para ejecutar cada 10 minutos:
*/10 * * * * $HOME/sistema_ok.sh

# 5. Verificar
crontab -l

# 6. Monitorear
tail -f ~/sistema_ok.log
```

Otros intervalos útiles:
```
*/10 * * * * = Cada 10 minutos
*/15 * * * * = Cada 15 minutos
0,10,20,30,40,50 * * * * = Cada 10 minutos (alternativa)
0-59/10 * * * * = Cada 10 minutos (alternativa)
```

9. Crea un script que genere un archivo con la fecha actual. Prográmalo para ejecutarse el primer día de cada mes a medianoche.

```bash
#!/bin/bash
# Nombre: reporte_mensual.sh
# Descripción: Genera archivo de reporte mensual

# Directorio de reportes
dir_reportes="$HOME/reportes_mensuales"
mkdir -p "$dir_reportes"

# Generar nombre de archivo con fecha
fecha=$(date '+%Y-%m-%d')
mes_anio=$(date '+%Y-%m')
archivo="$dir_reportes/reporte_${mes_anio}.txt"

# Crear contenido del reporte
{
    echo "======================================"
    echo "REPORTE MENSUAL"
    echo "======================================"
    echo "Fecha de generación: $fecha"
    echo "Hora: $(date '+%H:%M:%S')"
    echo ""
    echo "Sistema: $(uname -s)"
    echo "Usuario: $USER"
    echo "Hostname: $(hostname)"
    echo ""
    echo "Directorio home: $HOME"
    echo "Espacio en disco:"
    df -h "$HOME" | tail -1
    echo ""
    echo "======================================"
} > "$archivo"

# Log de ejecución
log_file="$HOME/reportes_mensuales/ejecucion.log"
echo "[$(date '+%Y-%m-%d %H:%M:%S')] Reporte mensual generado: $archivo" >> "$log_file"
```

Configurar crontab:
```bash
# 1. Crear el script
nano ~/reporte_mensual.sh
chmod +x ~/reporte_mensual.sh

# 2. Probar manualmente
~/reporte_mensual.sh
ls -lh ~/reportes_mensuales/
cat ~/reportes_mensuales/reporte_*.txt

# 3. Editar crontab
crontab -e

# 4. Añadir para ejecutar el día 1 de cada mes a medianoche:
0 0 1 * * $HOME/reporte_mensual.sh

# 5. Verificar
crontab -l
```

Explicación de cron mensual:
```
0 0 1 * * = Día 1 de cada mes a medianoche
0 0 15 * * = Día 15 de cada mes a medianoche
0 0 1,15 * * = Día 1 y 15 de cada mes a medianoche
0 0 1 1 * = El 1 de enero a medianoche (anualmente)
0 0 1 */3 * = Primer día cada 3 meses (trimestral)
0 0 L * * = Último día del mes (en algunos cron, no todos)
```

10. Configura un script que escriba "Probando cron" en un archivo. Después, buscar información para revisar los logs del sistema y confirmar su ejecución.

```bash
#!/bin/bash
# Nombre: probar_cron.sh
# Descripción: Script de prueba para verificar cron

# Archivo de salida
archivo="$HOME/prueba_cron.log"

# Escribir mensaje
echo "[$(date '+%Y-%m-%d %H:%M:%S')] Probando cron - Ejecución exitosa" >> "$archivo"

# Escribir también en salida estándar para que aparezca en logs de cron
echo "Cron ejecutado correctamente a las $(date '+%H:%M:%S')"
```

Configurar y verificar:
```bash
# 1. Crear el script
nano ~/probar_cron.sh
chmod +x ~/probar_cron.sh

# 2. Probar manualmente
~/probar_cron.sh
cat ~/prueba_cron.log

# 3. Editar crontab
crontab -e

# 4. Añadir para ejecutar cada 5 minutos (para prueba rápida):
*/5 * * * * $HOME/probar_cron.sh

# 5. Verificar que se añadió
crontab -l
```

Revisar logs del sistema para confirmar ejecución:

En Linux:
```bash
# Ver logs de cron (varias ubicaciones según distribución)
sudo tail -f /var/log/cron
sudo tail -f /var/log/cron.log
sudo tail -f /var/log/syslog | grep CRON

# Buscar ejecuciones de tu script
grep probar_cron /var/log/syslog
grep CRON /var/log/syslog | grep $USER

# Ver logs con journalctl (systemd)
sudo journalctl -u cron.service -f
sudo journalctl -u cron.service --since "10 minutes ago"
```

En macOS:
```bash
# Ver logs de cron en macOS
log show --predicate 'process == "cron"' --last 1h
log show --predicate 'eventMessage contains "probar_cron"' --last 30m

# Logs del sistema
tail -f /var/log/system.log | grep cron

# Verificar que cron está corriendo
ps aux | grep cron
```

Comandos útiles para debugging:
```bash
# Ver tu crontab actual
crontab -l

# Ver el archivo de salida del script
cat ~/prueba_cron.log

# Ver en tiempo real las nuevas líneas
tail -f ~/prueba_cron.log

# Verificar permisos del script
ls -l ~/probar_cron.sh

# Verificar que cron está activo
# Linux:
sudo systemctl status cron
# o
sudo service cron status

# macOS:
sudo launchctl list | grep cron

# Ver todas las tareas cron del sistema (root)
sudo crontab -l

# Editar variables de entorno en crontab (si necesario)
crontab -e
# Añadir al inicio:
# PATH=/usr/local/bin:/usr/bin:/bin
# SHELL=/bin/bash
```

Troubleshooting común:
```bash
# Si cron no ejecuta el script:

# 1. Verificar que el script tiene permisos de ejecución
chmod +x ~/probar_cron.sh

# 2. Usar rutas absolutas en crontab
# ✓ Correcto: /home/usuario/probar_cron.sh
# ✗ Incorrecto: ~/probar_cron.sh

# 3. Redirigir salida y errores para debug
*/5 * * * * $HOME/probar_cron.sh >> $HOME/cron_debug.log 2>&1

# 4. Verificar que el servicio cron está corriendo
sudo systemctl start cron  # Linux
# En macOS cron siempre está activo

# 5. Verificar sintaxis del crontab
# Después de editar, si hay errores, crontab te avisará
```