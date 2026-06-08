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

Locale = la "cultura" que entiende la computadora (idioma + formato + caracteres).

El código configura el sistema para usar inglés de EE.UU. con caracteres universales (UTF-8), evitando errores en programas que necesitan mostrar texto con tildes o emojis.

Setup Sources

You will need to add the ROS 2 apt repository to your system.

First ensure that the Ubuntu Universe repository is enabled.

sudo apt install software-properties-common
sudo add-apt-repository universe

Now add the ROS 2 GPG key with apt.

sudo apt update && sudo apt install curl -y
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg

Then add the repository to your sources list.

echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null

¿Qué es un APT repository?

Imagina que APT (Advanced Package Tool) es como una tienda de apps para Ubuntu/Debian. Un repository (repositorio) es el catálogo de esa tienda.

· Sin repositorios → solo tienes lo que ya vino instalado
· Con repositorios → puedes descargar e instalar cualquier programa desde Internet

Ejemplo: cuando haces sudo apt install python3, APT busca en sus repositorios configurados, descarga Python y lo instala automáticamente.

¿Qué hace el código?

Este código agrega el repositorio oficial de ROS 2 a tu sistema, para que puedas instalarlo como cualquier otro programa.

Paso 1: Habilitar "Universe" repository

```bash
sudo apt install software-properties-common
sudo add-apt-repository universe
```

· universe = repositorio comunitario con miles de programas de código abierto
· software-properties-common = herramienta para manejar repositorios fácilmente

Paso 2: Agregar la llave GPG de ROS 2

```bash
sudo apt update && sudo apt install curl -y
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg
```

¿Qué es una llave GPG? Es como un sello de autenticidad. Garantiza que los archivos vienen realmente de ROS 2 y no de un hacker.

Sin la llave, APT rechazaría instalar paquetes de ROS por seguridad.

Paso 3: Agregar el repositorio a tu lista de fuentes

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
```

Traducción:

· deb = repositorio de paquetes binarios
· arch=... = solo para tu arquitectura (amd64, arm64, etc.)
· signed-by=... = usa esta llave GPG para verificar
· http://... = dónde están los paquetes (los servidores de ROS)
· $(lsb_release -cs) = tu versión de Ubuntu (ej: focal para 20.04, jammy para 22.04)
· /etc/apt/sources.list.d/ros2.list = archivo donde se guarda esta configuración

Paso 4: Actualizar e instalar ROS 2

```bash
sudo apt update
sudo apt install ros-humble-desktop
```

· sudo apt update = refresca el catálogo (ahora incluye ROS 2)
· sudo apt install ros-humble-desktop = instala ROS 2 completo

Analogía simple

Concepto Analogía
APT El instalador de apps de Ubuntu
Repository Una tienda de apps (como Google Play)
GPG key El certificado de seguridad de la tienda
sources.list Tu lista de tiendas favoritas
sudo apt update Refrescar qué apps están disponibles
sudo apt install Descargar e instalar una app

¿Por qué no instalas ROS 2 con sudo apt install ros-humble-desktop directamente?

Porque ROS 2 no está en los repositorios oficiales de Ubuntu. Primero debes agregar su repositorio, igual que agregarías la tienda de Samsung en tu teléfono si no viene preinstalada.

Resumen

El código configura una nueva tienda de apps (el repositorio de ROS 2) con su certificado de seguridad (llave GPG), para que puedas instalar ROS 2 como si fuera un programa normal de Ubuntu. Sin esto, APT no sabría dónde encontrar ROS 2.

