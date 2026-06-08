# ROS2-Foxy

locale  # check for UTF-8

sudo apt update && sudo apt install locales

sudo locale-gen en_US en_US.UTF-8

sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8

export LANG=en_US.UTF-8

locale  # verify settings

¿Qué es un locale?

Imagina que tu computadora es una persona que puede hablar muchos idiomas y seguir distintas costumbres del mundo. 
El locale es como la configuración regional que le dice:

· En qué idioma mostrarte los mensajes
· Formato de fechas (día/mes/año o mes/día/año)
· Cómo mostrar números (1,000.50 o 1.000,50)
· Qué alfabeto/caracteres usar (UTF-8 permite ñ, ç, emojis, etc.)

Ejemplo práctico:

· en_US.UTF-8 → inglés como en Estados Unidos, con soporte UTF-8
· es_MX.UTF-8 → español como en México, con UTF-8

Paso 1: Ver tu locale actual

```bash
locale  # muestra tu configuración actual
```

Si ves POSIX o C, significa que estás en modo mínimo (sin idioma completo).

Paso 2: Instalar los paquetes de locales

```bash
sudo apt update && sudo apt install locales
```

Esto instala las herramientas para manejar configuraciones regionales.

Paso 3: Generar los locales que quieres

```bash
sudo locale-gen en_US en_US.UTF-8
```

Esto crea los archivos para inglés de EE.UU. con y sin UTF-8.

Paso 4: Configurar como predeterminados

```bash
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
```

Esto le dice al sistema: "usa inglés de EE.UU. con UTF-8 para TODO".

Paso 5: Aplicar sin reiniciar

```bash
export LANG=en_US.UTF-8
```

Esto cambia la variable para la sesión actual.

Paso 6: Verificar

```bash
locale  # debería mostrar todo como en_US.UTF-8
```

¿Por qué es importante UTF-8?

UTF-8 permite usar cualquier carácter del mundo: ñ, ç, á, 界. 
El locale POSIX solo entiende caracteres básicos ingleses (ASCII).

Si intentas usar UTF-8 sin configurarlo bien, verás errores como:

```
-bash: warning: setlocale: LC_ALL: cannot change locale
```

Resumen 

Locale = la "cultura" que entiende tu computadora (idioma + formato + caracteres).

El código configura el sistema para usar inglés de EE.UU. con caracteres universales (UTF-8), evitando errores en programas que necesitan mostrar texto con tildes o emojis.
