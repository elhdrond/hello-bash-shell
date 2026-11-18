# ADMINISTRACIÓN DEL SISTEMA

## Posibles correcciones (ten en cuenta que pueden variar dependiendo de tu sistema operativo y directorios existentes)

1. Crea un archivo y visualiza sus permisos.

```bash
# Crear un archivo
touch mi_archivo.txt

# Visualizar sus permisos con ls -l
ls -l mi_archivo.txt

# Salida ejemplo: -rw-r--r-- 1 usuario grupo 0 Nov 1 10:00 mi_archivo.txt
# Donde:
# - primer carácter: tipo (- = archivo, d = directorio)
# - rw- = permisos del propietario (lectura, escritura)
# - r-- = permisos del grupo (solo lectura)
# - r-- = permisos de otros (solo lectura)

# Ver permisos en formato octal/numérico
stat -f "%A %N" mi_archivo.txt  # macOS
# o
stat -c "%a %n" mi_archivo.txt  # Linux
```

2. Otorga permisos de ejecución sólo al propietario en modo simbólico.

```bash
# Añadir permisos de ejecución solo al propietario (user)
chmod u+x mi_archivo.txt

# Verificar los cambios
ls -l mi_archivo.txt
# Ahora mostrará: -rwxr--r-- (la x indica ejecución para el propietario)

# Explicación del modo simbólico:
# u = user (propietario)
# g = group (grupo)
# o = others (otros)
# a = all (todos)
# + = añadir permiso
# - = quitar permiso
# = = establecer exactamente estos permisos
# r = read (lectura)
# w = write (escritura)
# x = execute (ejecución)
```

3. Cambia sus permisos a 644.

```bash
# Cambiar permisos a 644 en modo numérico/octal
chmod 644 mi_archivo.txt

# Verificar los cambios
ls -l mi_archivo.txt
# Mostrará: -rw-r--r--

# Explicación del modo numérico:
# 644 significa:
# 6 (110 en binario) = rw- = lectura y escritura para el propietario
# 4 (100 en binario) = r-- = solo lectura para el grupo
# 4 (100 en binario) = r-- = solo lectura para otros

# Tabla de valores:
# 0 = --- (sin permisos)
# 1 = --x (ejecución)
# 2 = -w- (escritura)
# 3 = -wx (escritura y ejecución)
# 4 = r-- (lectura)
# 5 = r-x (lectura y ejecución)
# 6 = rw- (lectura y escritura)
# 7 = rwx (todos los permisos)
```

4. Elimina los permisos para el grupo.

```bash
# Eliminar todos los permisos del grupo con modo simbólico
chmod g-rwx mi_archivo.txt
# O más simple (eliminar todos los permisos del grupo):
chmod g= mi_archivo.txt

# Verificar los cambios
ls -l mi_archivo.txt
# Mostrará: -rw----r-- (el grupo ya no tiene permisos)

# Alternativa con modo numérico (de 644 a 604):
chmod 604 mi_archivo.txt

# Otras formas de quitar permisos específicos al grupo:
# chmod g-r mi_archivo.txt  # quitar solo lectura
# chmod g-w mi_archivo.txt  # quitar solo escritura
# chmod g-x mi_archivo.txt  # quitar solo ejecución
```

5. Haz que sólo pueda ejecutarse por el propietario.

```bash
# Establecer permisos para que solo el propietario pueda ejecutar
# Modo numérico: 700 (rwx para propietario, nada para grupo y otros)
chmod 700 mi_archivo.txt

# Verificar los cambios
ls -l mi_archivo.txt
# Mostrará: -rwx------ (solo el propietario tiene todos los permisos)

# Alternativa con modo simbólico:
chmod u=rwx,g=,o= mi_archivo.txt
# O desde permisos existentes:
chmod u+rwx,go-rwx mi_archivo.txt

# Si solo quieres dar ejecución (manteniendo lectura/escritura existentes):
chmod u+x,go-x mi_archivo.txt

# Permisos comunes para scripts ejecutables solo por el propietario:
# 700 = rwx------ (todos los permisos solo para el propietario)
# 500 = r-x------ (lectura y ejecución, sin escritura)
```

6. Crea una carpeta y dale permisos para que sólo el usuario pueda acceder.

```bash
# Crear una carpeta
mkdir mi_carpeta_privada

# Darle permisos solo para el propietario (700)
chmod 700 mi_carpeta_privada

# Verificar los permisos
ls -ld mi_carpeta_privada
# Mostrará: drwx------ (d indica directorio)

# Crear carpeta con permisos específicos en un solo comando
mkdir -m 700 nueva_carpeta_privada

# Explicación para directorios:
# r (lectura) = poder listar el contenido del directorio
# w (escritura) = poder crear/eliminar archivos dentro
# x (ejecución) = poder acceder/entrar al directorio

# Sin el permiso x, no puedes entrar al directorio aunque tengas r y w
# Por eso 700 (rwx------) es lo correcto para carpetas privadas
```

7. Cámbiale el propietario a otro usuario de tu sistema (si existe y tienes permisos).

```bash
# Cambiar el propietario del archivo (requiere permisos de root/sudo)
sudo chown otro_usuario mi_archivo.txt

# Verificar el cambio
ls -l mi_archivo.txt

# Cambiar propietario de un directorio
sudo chown otro_usuario mi_carpeta_privada

# Cambiar propietario recursivamente (directorio y todo su contenido)
sudo chown -R otro_usuario mi_carpeta_privada

# Cambiar propietario y grupo al mismo tiempo
sudo chown otro_usuario:otro_grupo mi_archivo.txt

# Solo cambiar el grupo (también se puede usar chgrp)
sudo chown :nuevo_grupo mi_archivo.txt
# O equivalente:
sudo chgrp nuevo_grupo mi_archivo.txt

# Ver usuarios disponibles en el sistema
cat /etc/passwd | cut -d: -f1

# Ver grupos disponibles
cat /etc/group | cut -d: -f1

# Nota: En macOS, usuarios comunes pueden ser: root, nobody
# En Linux: root, www-data, nobody, etc.
```

8. Consulta la máscara de permisos actual y calcula qué permisos por defecto tendrán los nuevos archivos.

```bash
# Consultar la máscara de permisos actual (umask)
umask

# Mostrar en formato simbólico
umask -S

# Cálculo de permisos por defecto:
# La umask RESTA permisos de los permisos base
# - Archivos nuevos parten de 666 (rw-rw-rw-)
# - Directorios nuevos parten de 777 (rwxrwxrwx)

# Ejemplo: si umask es 0022
# Para archivos: 666 - 022 = 644 (rw-r--r--)
# Para directorios: 777 - 022 = 755 (rwxr-xr-x)

# Ejemplo: si umask es 0002
# Para archivos: 666 - 002 = 664 (rw-rw-r--)
# Para directorios: 777 - 002 = 775 (rwxrwxr-x)

# Ejemplo: si umask es 0077
# Para archivos: 666 - 077 = 600 (rw-------)
# Para directorios: 777 - 077 = 700 (rwx------)

# Probar creando un archivo
touch test_umask.txt
ls -l test_umask.txt
rm test_umask.txt

# Probar creando un directorio
mkdir test_umask_dir
ls -ld test_umask_dir
rmdir test_umask_dir
```

9. Cambia la máscara, crea un archivo y consulta los permisos por defecto del archivo.

```bash
# Ver la máscara actual
umask
# Supongamos que muestra: 0022

# Cambiar la máscara a 0077 (más restrictiva - solo propietario)
umask 0077

# Verificar el cambio
umask
# Mostrará: 0077

# Crear un archivo con la nueva máscara
touch archivo_con_nueva_umask.txt

# Consultar los permisos del archivo
ls -l archivo_con_nueva_umask.txt
# Mostrará: -rw------- (600)
# Porque 666 - 077 = 600

# Crear un directorio con la nueva máscara
mkdir directorio_con_nueva_umask

# Consultar los permisos del directorio
ls -ld directorio_con_nueva_umask
# Mostrará: drwx------ (700)
# Porque 777 - 077 = 700

# Restaurar la máscara original
umask 0022

# Verificar
umask

# Nota: El cambio de umask solo afecta a la sesión actual
# Para hacerlo permanente, añádelo a ~/.bashrc o ~/.zshrc:
# echo "umask 0077" >> ~/.bashrc
```

10. Utiliza un comando como superusuario.

```bash
# Usar sudo para ejecutar un comando como superusuario
sudo ls -la /root

# Te pedirá tu contraseña (no la del root, sino la tuya)

# Otros ejemplos de comandos con sudo:

# Instalar paquetes (Linux)
sudo apt-get update  # Debian/Ubuntu
sudo yum update      # RedHat/CentOS

# Instalar paquetes (macOS)
sudo brew install tree

# Editar archivos del sistema
sudo nano /etc/hosts

# Ver archivos de log del sistema
sudo tail -f /var/log/system.log  # macOS
sudo tail -f /var/log/syslog      # Linux

# Cambiar permisos de archivos del sistema
sudo chmod 755 /usr/local/bin/mi_script.sh

# Cambiar propietario
sudo chown root:root archivo.txt

# Cambiar a modo superusuario interactivo (¡CUIDADO!)
sudo su
# O
sudo -i

# Ejecutar múltiples comandos como root
sudo sh -c 'comando1 && comando2 && comando3'

# Ver comandos sudo ejecutados recientemente
sudo cat /var/log/auth.log | grep sudo  # Linux
sudo cat /var/log/system.log | grep sudo  # macOS

# Limpiar la caché de contraseñas de sudo
sudo -k

# Ver qué comandos puedes ejecutar con sudo
sudo -l
```