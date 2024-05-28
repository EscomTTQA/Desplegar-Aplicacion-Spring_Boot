# Desplegar-Aplicacion-Spring_Boot
Se describe el proceso de despliegue de una aplicación Spring Boot y una base de datos con MySQL en una instancia EC2 de Amazon Web Services (AWS).

## Preparativos Previos al Despliegue
Antes del despliegue, se realizaron las siguientes configuraciones:

### Creación de la instancia EC2 utilizando la imagen de Amazon Linux 2023.
Instalación de Java siguiendo las instrucciones oficiales de Amazon Corretto 17.[Documentación de instalación] (https://docs.aws.amazon.com/es_es/corretto/latest/corretto-17-ug/amazon-linux-install.html).
O simplemente, una vez coectado a la instancia de EC2 creada mediante la consola, ejecutar el siguiente comando:

```bash
sudo yum install java-17-amazon-corretto-devel
```

Proceso de Instalación y Configuración
Una vez conectados a la instancia de Amazon Linux 2023, se ejecutaron los siguientes comandos:

cd /home/ec2-user

Descripción: Cambia el directorio de trabajo al directorio del usuario ec2-user.
Propósito: Establecer un entorno de trabajo adecuado para las próximas operaciones.
sudo wget https://dev.mysql.com/get/mysql84-community-release-el9-1.noarch.rpm

Descripción: Descarga el paquete RPM de MySQL 8.4 desde el sitio oficial de MySQL.
Propósito: Obtener el paquete necesario para habilitar el repositorio de MySQL en el sistema.
sudo yum install mysql84-community-release-el9-1.noarch.rpm

Descripción: Instala el paquete RPM descargado.
Propósito: Configurar el repositorio de MySQL en el sistema.
sudo yum install mysql-community-server

Descripción: Instala el servidor MySQL desde el repositorio configurado.
Propósito: Instalar MySQL en la instancia EC2, que servirá como base de datos para la aplicación Spring Boot.
sudo systemctl start mysqld

Descripción: Inicia el servicio de MySQL.
Propósito: Poner en funcionamiento el servidor MySQL.
sudo systemctl status mysqld

Descripción: Verifica el estado del servicio de MySQL.
Propósito: Asegurarse de que MySQL se ha iniciado correctamente y está en ejecución sin problemas.
Despliegue de la Aplicación Spring Boot
Con la instancia configurada y MySQL en funcionamiento, se realizaron los siguientes pasos para desplegar la aplicación Spring Boot:

Transferencia del archivo JAR de la aplicación a la instancia EC2.
Configuración del archivo de propiedades de la aplicación para conectarse a la base de datos MySQL.
Ejecución de la aplicación utilizando el comando:
sh
java -jar nombre-de-la-aplicacion.jar
