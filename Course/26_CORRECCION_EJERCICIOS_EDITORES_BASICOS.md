# EDITORES BÁSICOS

## Posibles correcciones (ten en cuenta que pueden variar dependiendo de tu sistema operativo y directorios existentes)

### nano

1. Crea un archivo llamado nota.txt y escribe tres líneas de texto.

**Solución:**
```bash
# Abrir nano con el archivo nota.txt
nano nota.txt

# Una vez dentro de nano:
# - Escribe tus tres líneas de texto, por ejemplo:
#   Esta es la primera línea
#   Esta es la segunda línea
#   Esta es la tercera línea
# - Presiona Ctrl + O (WriteOut) para guardar
# - Presiona Enter para confirmar el nombre del archivo
# - Presiona Ctrl + X para salir
```

2. Abre nota.txt, añade una línea al final y guarda los cambios.

**Solución:**
```bash
# Abrir el archivo existente
nano nota.txt

# Una vez dentro:
# - Mueve el cursor al final del archivo con Ctrl + V (o flechas)
# - Añade una nueva línea: "Esta es la cuarta línea"
# - Presiona Ctrl + O para guardar
# - Presiona Enter para confirmar
# - Presiona Ctrl + X para salir
```

3. Abre un archivo nuevo llamado recordatorio.txt, escribe algo y sal sin guardar.

**Solución:**
```bash
# Abrir nano con el nuevo archivo
nano recordatorio.txt

# Una vez dentro:
# - Escribe cualquier texto: "Este es un recordatorio temporal"
# - Presiona Ctrl + X para salir
# - Cuando pregunte "Save modified buffer?", presiona N (No)
# - El archivo no se guardará y nano se cerrará
```

4. Busca una palabra específica en un archivo existente.

**Solución:**
```bash
# Abrir un archivo existente
nano nota.txt

# Una vez dentro:
# - Presiona Ctrl + W (Where is / buscar)
# - Escribe la palabra que quieres buscar, por ejemplo: "segunda"
# - Presiona Enter
# - El cursor se moverá a la primera ocurrencia
# - Para buscar la siguiente ocurrencia, presiona Ctrl + W y luego Enter
# - Presiona Ctrl + X para salir
```

5. Corta una línea y pégala en otra parte.

**Solución:**
```bash
# Abrir el archivo
nano nota.txt

# Una vez dentro:
# - Mueve el cursor a la línea que quieres cortar
# - Presiona Ctrl + K (Kill/Cortar) para cortar la línea completa
# - Mueve el cursor a donde quieres pegar la línea
# - Presiona Ctrl + U (Uncut/Pegar) para pegar la línea
# - Presiona Ctrl + O para guardar, Enter para confirmar
# - Presiona Ctrl + X para salir

# Nota: Puedes presionar Ctrl + K múltiples veces para cortar varias líneas
# y luego Ctrl + U una vez para pegarlas todas juntas
```

### vim

6. Crea apuntes.txt, entra en modo inserción y escribe una frase.

**Solución:**
```bash
# Abrir vim con el archivo apuntes.txt
vim apuntes.txt

# Una vez dentro de vim:
# - Por defecto estás en modo NORMAL
# - Presiona i para entrar en modo INSERT (inserción)
# - Verás "-- INSERT --" en la parte inferior
# - Escribe una frase, por ejemplo: "Estos son mis apuntes de Bash"
# - Presiona Esc para volver al modo NORMAL
# - Escribe :wq y presiona Enter para guardar y salir
#   (w = write/guardar, q = quit/salir)
```

7. Mueve el cursor sin usar las flechas.

**Solución:**
```bash
# Abrir el archivo en vim
vim apuntes.txt

# En modo NORMAL (presiona Esc si estás en otro modo):
# Movimientos básicos:
# - h = mover a la izquierda
# - j = mover abajo
# - k = mover arriba
# - l = mover a la derecha

# Movimientos por palabra:
# - w = siguiente palabra (word)
# - b = palabra anterior (back)
# - e = final de palabra (end)

# Movimientos de línea:
# - 0 = inicio de la línea
# - $ = final de la línea
# - ^ = primer carácter no blanco de la línea

# Movimientos de archivo:
# - gg = ir al inicio del archivo
# - G = ir al final del archivo
# - :10 = ir a la línea 10

# Practica estos movimientos y luego sal con :q
```

8. Borra una línea completa y deshaz el cambio.

**Solución:**
```bash
# Abrir el archivo en vim
vim apuntes.txt

# En modo NORMAL (presiona Esc):
# - Coloca el cursor en cualquier línea
# - Presiona dd para borrar la línea completa
# - La línea se borrará

# Para deshacer el cambio:
# - Presiona u (undo)
# - La línea reaparecerá

# Otros comandos de borrado útiles:
# - x = borrar un carácter
# - dw = borrar una palabra
# - d$ = borrar desde el cursor hasta el final de la línea
# - D = igual que d$ (borrar hasta el final)

# Para rehacer (opuesto a deshacer):
# - Presiona Ctrl + r (redo)

# Sal sin guardar con :q!
```

9. Copia una línea y pégala debajo.

**Solución:**
```bash
# Abrir el archivo en vim
vim apuntes.txt

# En modo NORMAL (presiona Esc):
# - Coloca el cursor en la línea que quieres copiar
# - Presiona yy para copiar (yank) la línea completa
# - Mueve el cursor a donde quieres pegar
# - Presiona p para pegar debajo de la línea actual
#   (o P para pegar arriba de la línea actual)

# Otros comandos de copia útiles:
# - yw = copiar una palabra
# - y$ = copiar desde el cursor hasta el final de la línea
# - 3yy = copiar 3 líneas

# Copiar y cortar:
# - yy copia (yank)
# - dd corta (delete), pero también lo guarda para pegar
# - p pega (put/paste)

# Guarda con :w o sal con :q! si no quieres guardar
```

10. Guarda los cambios y sal.

**Solución:**
```bash
# Estando en vim con cambios realizados:

# En modo NORMAL (presiona Esc):
# - Escribe :wq y presiona Enter
#   (write + quit = guardar y salir)

# Alternativas:
# - :x = guardar y salir (igual que :wq)
# - :w = solo guardar, sin salir
# - :q = solo salir (si no hay cambios)
# - :q! = salir sin guardar (forzar)
# - :wq! = guardar y salir forzado
# - ZZ = guardar y salir (en modo NORMAL, sin necesidad de :)
# - ZQ = salir sin guardar (en modo NORMAL)

# Guardar con nombre diferente:
# - :w nuevo_nombre.txt = guardar como nuevo archivo
# - :saveas nuevo_nombre.txt = guardar como y abrir el nuevo archivo

# Si el archivo es de solo lectura:
# - :w! = forzar escritura (si tienes permisos)
# - :w !sudo tee % = guardar con sudo
```