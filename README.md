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

