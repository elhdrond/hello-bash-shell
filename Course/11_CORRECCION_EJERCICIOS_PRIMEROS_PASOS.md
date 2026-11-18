# PRIMEROS PASOS

## Posibles correcciones (ten en cuenta que pueden variar dependiendo de tu sistema operativo y directorios existentes)

1. En la terminal, muestra el directorio en el que estás ahora.

```bash
pwd
```

2. Cambia al directorio Documentos (o Documents) de tu sistema.

```bash
cd ~/Documents
```

3. Vuelve al mismo directorio (Documentos o Documents), pero esta vez usando una ruta absoluta completa.

```bash
cd /Users/braismoure/Documents
```

4. Sube un nivel en la jerarquía de directorios.

```bash
cd ..
```

5. Lista el contenido del directorio actual en formato simple, luego largo y finalmente incluyendo archivos ocultos.

```bash
# Formato simple
ls

# Formato largo
ls -l

# Incluyendo archivos ocultos
ls -la
```

6. Consulta el manual de algún comando.

```bash
man ls
# Para salir del manual, presiona 'q'
```

7. Consulta la ayuda de algún comando.

```bash
ls --help
# o también:
help cd
```

8. Muestra tu nombre de usuario, la fecha, hora actuales y el calendario de este mes.

```bash
# Nombre de usuario
whoami

# Fecha y hora actuales
date

# Calendario del mes actual
cal
```

9. Regresa al directorio donde comenzaste en el primer ejercicio.

```bash
cd -
# o volver al directorio home:
cd ~
# o simplemente:
cd
```

11. Limpia la pantalla.

```bash
clear
```