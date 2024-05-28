# Desplegar-Aplicacion-Spring_Boot
Se describe el proceso de despliegue de una aplicación Spring Boot y una base de datos con MySQL en una instancia EC2 de Amazon Web Services (AWS).

## Preparativos Previos al Despliegue de la apliacación Java y la base de datos de MySQL
Antes del despliegue, se realizaron las siguientes configuraciones:

### Creación de la instancia EC2 utilizando la imagen de Amazon Linux 2023.
Inicia sesión en AWS. Luego, en los servicios que se ofrecen seleccionar EC2, dar clic a:
![image](https://github.com/EscomTTQA/Desplegar-Aplicacion-Spring_Boot/assets/167526018/7807a72a-e42a-4db9-88e8-4c7241802f64)

Se te mostrará una interfaz como la siguiente, donde podrás seleccionar distintas opciones, como por ejemplo la AMI (Amazon Machine Image) que es una plantilla que contiene la configuración de software (sistema operativo, servidor de aplicaciones y aplicaciones) necesaria para lanzar la instancia, de las cuales hay muchas opciones, tanto creadas u ofreciadas por AWS o generadas por algún usuario u organización que son expuestas para poder usarlas. Para el caso del proyecto se usa la AMI de Amazon Linux:
![image](https://github.com/EscomTTQA/Desplegar-Aplicacion-Spring_Boot/assets/167526018/9a5e01ed-edcf-4e32-befb-cbe5b73c459a)

Para poder desplegar la aplicación de Spring Boot se requiere la instalación de Java se siguen las instrucciones oficiales de Amazon Corretto 17. [Documentación de instalación](https://docs.aws.amazon.com/es_es/corretto/latest/corretto-17-ug/amazon-linux-install.html). Esto debido a que la aplicación desarrollada usa Java 17, sin embargo si el desarrollo de un proyecto Java se pudiera construir y empaquetar con la versión 11, en AWS hay imágenes de aplicaciones y sistemas operativos que ya tienen instalado lo necesario para ejecutar una aplicación como esta, por eso es importante la elección de la máquina de Amazon.  

Una vez coectado a la instancia de EC2 creada mediante la consola, ejecutar el siguiente comando (tomado de la documentación antes mencionada):

```bash
sudo yum install java-17-amazon-corretto-devel
```
Debería de mostrarse resultados como los siguientes:
![image](https://github.com/EscomTTQA/Desplegar-Aplicacion-Spring_Boot/assets/167526018/34067f7e-c214-4a1e-a95f-eab146f880d1)

## Proceso de Instalación y Configuración
Una vez conectados a la instancia de Amazon Linux 2023, se ejecutaron los siguientes comandos:

```bash
cd /home/ec2-user
```
1. **Descripción**: Cambia el directorio de trabajo al directorio del usuario ec2-user.
2. **Propósito**: Establecer un entorno de trabajo adecuado para las próximas operaciones.

```bash
sudo wget https://dev.mysql.com/get/mysql84-community-release-el9-1.noarch.rpm
```
1. **Descripción**: Descarga el paquete RPM de MySQL 8.4 desde el sitio oficial de MySQL.
2. **Propósito**: Obtener el paquete necesario para habilitar el repositorio de MySQL en el sistema.

```bash
sudo yum install mysql84-community-release-el9-1.noarch.rpm
```
1. **Descripción**: Instala el paquete RPM descargado.
2. **Propósito**: Configurar el repositorio de MySQL en el sistema.

```bash
sudo yum install mysql-community-server
```

1. **Descripción**: Instala el servidor MySQL desde el repositorio configurado.
2. **Propósito**: Instalar MySQL en la instancia EC2, que servirá como base de datos para la aplicación Spring Boot.

```bash
sudo systemctl start mysqld
```

1. **Descripción**: Inicia el servicio de MySQL.
2. **Propósito**: Poner en funcionamiento el servidor MySQL.

```bash
sudo systemctl status mysqld
```

1. **Descripción**: Verifica el estado del servicio de MySQL.
2. **Propósito**: Asegurarse de que MySQL se ha iniciado correctamente y está en ejecución sin problemas.

## Despliegue de la Aplicación Spring Boot
Con la instancia configurada y MySQL en funcionamiento, se realizaron los siguientes pasos para desplegar la aplicación Spring Boot:

* Transferencia del archivo JAR de la aplicación a la instancia EC2.
* Configuración del archivo de propiedades de la aplicación para conectarse a la base de datos MySQL.
* Ejecución de la aplicación utilizando el comando:

```sh
java -jar nombre-de-la-aplicacion.jar
```
