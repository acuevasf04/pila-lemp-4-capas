# PILA LEMP DE 4 CAPAS

<img width="811" height="510" alt="clienteservidor" src="https://github.com/user-attachments/assets/4ac200dd-ba55-42ff-8f05-b0082488c84a" />

## ÍNDICE
1. INTRODUCCIÓN
2. ARQUITECTURA DE LA INFRAESTRUCTURA
3. CONFIGURACIÓN DE LAS MÁQUINAS
   1. BALANCEADOR
   2. SERVIDORES BACKEND Y NFS
   3. HAPROXY
   4. SERVIDORES MARIADB

## 1. INTRODUCCIÓN 
En esta práctica, se tendrá como objetivo la configuración total de una pila de arquitectura LEMP de 4 capas, con el uso de 1 balanceador de carga con acceso a internet, 2 servidores backend, 1 servidor NFS, un balanceador HaProxy y 2 servidores de Base de Datos con MariaDB. Teniendo en cuenta de que el balanceador es el único que tiene que tener acceso a internet.

## 2. ARQUITECTURA DE LA INFRAESTRUCTURA
La estructura del CMS de 4 capas es el siguiente, 1 balanceador de carga de con acceso a internet utilizando nginx, 2 servidores backend donde hostearan la página web de este trabajo, un servidor NFS el cual sincronizará los 2 servidores backend, un balanceador HaProxy el cual hará que se tengan acceso a los dos servidores de base de datos, y 2 servidores de base de datos con MariaDB donde se almacenaran los datos de la página que se está creando.

<img width="445" height="494" alt="imagen" src="https://github.com/user-attachments/assets/c1072fd9-8ac0-4d25-8255-c47b5e4299e3" />

## 3. CONFIGURACIÓN DE LAS MÁQUINAS

### 3.1. BALANCEADOR

Para la configuración del balanceador, primero hay que actualizar el repositorio de paquetes de Linux, para ello hay que usar el comando ```sudo apt update```, luego se instala el servicio de nginx con el comando ```sudo apt install -y nginx```.
Para entrar en los archivos de configuración, hay que entrar en la ruta ```/etc/nginx/sites-avalibles``` y desde ahí hacer una copia de la configuración por defecto (archivo default) con el comando ```sudo cp default cluster```. Ahora se entra en el archivo nuevo creado, y poner lo mismo de la imagen:
<img width="801" height="814" alt="imagen" src="https://github.com/user-attachments/assets/e76195d8-84d4-4a46-a233-49f8432b13c1" />
Con los comandos ```ln -sf /etc/nginx/sites-available/webapp /etc/nginx/sites-enabled/```y ```rm -f /etc/nginx/sites-enabled/default```se selecciona la configuración que se quiere enseñar y borrar la que está por defecto.

### 3.2. SERVIDORES BACKEND
Para la configuación de los servidores backend se hacen primero hay que actualizar el repositorio de paquetes de Linux, para ello hay que usar el comando ```sudo apt update```, luego se instala el servicio de nginx y la aplicación cliente del servidor nfs con el comando ```sudo apt install -y nginx nfs-common```.
Primero se configurará la aplicación cliente del servicio NFS, donde se creará primero una carpeta en donde se encontrará nuestra aplicación web. Para ello, se hará con el comando ```mkdir -p /var/www/html/webapp```. Luego se montará la carpeta con el comando ```mount -t nfs 192.168.20.10:/var/www/html/webapp /var/www/html/webapp```siendo la dirección IP del servidor NFS.
Para entrar en los archivos de configuración, hay que entrar en la ruta ```/etc/nginx/sites-avalibles``` y desde ahí hacer una copia de la configuración por defecto (archivo default) con el comando ```sudo cp default cluster```. Ahora se entra en el archivo nuevo creado, y poner lo mismo de la imagen:
<img width="929" height="637" alt="imagen" src="https://github.com/user-attachments/assets/d47456a7-c3f5-4a2f-ae64-c907820013d8" />
Con los comandos ```ln -sf /etc/nginx/sites-available/webapp /etc/nginx/sites-enabled/```y ```rm -f /etc/nginx/sites-enabled/default```se selecciona la configuración que se quiere enseñar y borrar la que está por defecto y se reinicia con el comando ```sudo systemctl restart nginx```y se verifica que funciona bien con ```sudo systemctl status nginx```
Esto se repetirá 2 veces ya que la idea es que los servidores hagan lo mismo.

### 3.3. SERVIDOR NFS
Para el servidor NFS, se hará primero el comando ```sudo apt update```para actualizar el repositorio de paquetes de Linux. Luego con el comando ```sudo apt install git mariadb-client nfs-kernel-server``` se instalará un cliente de MariaDB, el servicio de NFS y una conexión con git hub para la descarga de un archivo php. Luego, con el comando ```sudo apt install php-fpm php-mysql php-curl php-gd php-mbstring php-xml php-xmlrpc php-soap php-intl php-zip netcat-openbsd```se instalará todas las herramientas para el interprete de php.
A continuación, se creará la carpeta compartida con las máquinas backend para subir la aplicación web a la vez.
