# Introduction

This repository generates a LAMP stack on a single container, replicating a common web server. Additionally, some PHP components such as gettext, composer, and php-zip have been added.

Its intended use is as a template for creating a development enviroment where you have everything necesary to run a PHP aplication, including frameworks like Symfony or Laravel

# Usage

With docker and docker-compose running on the machine, run the docker-compose.yml file.

```
docker-compose -f "docker-compose.yml" up -d --build
```

By default, a site will start on port 80 and a MariaDB database in port 3306

## Variables
### Service Versions
These are the versions that will be used internally. This project does not support more than one version for each service.

```
PHP_VERSION=8.3
APACHE_VERSION=2.4.32
MYSQL_VERSION=5.6
```

### Image Names
This is the name that the Docker image of each service will take. If you need to have more than one environment running on the same machine, these must be modified along with the enabled ports.

```
PHP_NAME=php
APACHE_NAME=apache
MYSQL_NAME=mysql
```

### Network Name
This name will allow different containers within the same computer to use the services of another container. This is necessary if you want to have a single database server instance addressable from multiple containers.

```
NETWORK_NAME=local-network
```

### Database Parameters
Parameters to be used by the MariaDB server

```
DB_ROOT_PASSWORD=rootpassword
DB_NAME=local
DB_USERNAME=dbuser
DB_PASSWORD=password
MARIA_DB_PORT=3306
```

### Base Folder
Folder where the webpage files will be located.

```
PROJECT_ROOT=./src
```

### Ports to be used by the Apache server
These ports must be modified if you need to have more than one environment running on the same machine, along with the enabled ports.

The debug port can be used to configure xdebug

```
HTTP_PORT=80
FTP_PORT=21
DEBUG_PORT=9001
```

# Composer

It will be installed in the same image as PHP, The composer command can be run via SSH within the image's terminal.