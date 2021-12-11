# Introducción

Este repo es una copia del repositorio https://github.com/mzazon/PHP-apache-mysql-containerized el original es una demo generada para entender conceptos básicos de Docker levantando una aplicacion conocida (recomiendo leer el README original para entender como funciona la estructura de carpetas y los archivos de Docker)

Si bien este proyecto es muy similar en cuanto a la estructura de carpetas y funcionamiento, este repositorio esta pensado para usarse como espacio de desarrollo de PHP

Este repositorio genera una pila LAMP sobre un mismo contenedor, replicando un servidor web común
Ademas, se agregaron algunos componentes de PHP como gettext, composer y php-zip


# Instalación

Para poder empezar a utilizar el ambiente de desarrollo es necesario tener Docker instalado y completar las variables dentro de .env

Una vez completas, se debe ejecutar el archivo docker-compose.yml

```
docker-compose -f "docker-compose.yml" up -d --build
```


## Variables de entorno

[Nombre Variable]=[Valor default]

### versiónes de servicio
Son las versiónes que se van a usar internamente, este proyecto no soporta mas de una versión para cada servicio

```
PHP_VERSION=7.3
APACHE_VERSION=2.4.32
MYSQL_VERSION=5.6
```

### Nombres de imágenes
Este es el nombre que va a tomar la imagen de Docker de cada servicio, si se requiere tener mas de un ambiente corriendo en la misma maquina, deben modificarse junto con los puertos habilitados

```
PHP_NAME=php
APACHE_NAME=apache
MYSQL_NAME=mysql
```

### Nombre de la red
Este nombre va a permitir a contenedores distintos dentro del mismo equipo utilizar los servicios de otro contenedor, necesario si se quiere tener una única instancia del servidor MySQL direccionable desde varios contenedores

```
NETWORK_NAME=network
```

### Parámetros de MySQL
Parámetros   a utilizar por el servidor de MySQL

```
DB_ROOT_PASSWORD=rootpassword
DB_NAME=local
DB_USERNAME=dbuser
DB_PASSWORD=password
MYSQL_PORT=3306
```

### Carpeta base
Carpeta donde va a estar la base del servidor web, esta carpeta debe estar creada dentro del árbol de carpetas

```
PROJECT_ROOT=./public_html
```

### Puertos a utilizar por el servidor de apache
Estos puertos deben modificarse si se requiere tener mas de un ambiente corriendo en la misma maquina, junto con los puertos habilitados

El puerto de debug se puede utilizar para configurar xdebug

```
HTTP_PORT=80
FTP_PORT=21
DEBUG_PORT=9001
```

# Composer

Este contenedor instalara el composer de PHP para ser utilizado en caso de necesidad, el comando composer puede ejecutarse a través de SSH dentro de la imagen