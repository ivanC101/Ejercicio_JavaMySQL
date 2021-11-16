# Ejercicio_JavaMySQL
Ejercicio de la creación de una tabla en MySQL y su lectura desde Java para consultarla ordenando la tabla por apellidos, edad.

## Contenidos
* [General](#general)
* [Ajustes](#ajustes)
* [Instrucciones](#instrucciones)
* [Imágenes ejecución en Java](#imágenes)

## General
Serie de instrucciones y ajustes que se llevaron a cabo.

## Ajustes
Para correr este proyecto hay que modificar ``` mysqld.cnf ```:
* Hacer un respaldo de mysql.conf.d
```
$ cp /etc/mysql/mysql.conf.d/mysqld.cnf /etc/mysql/mysql.conf.d/mysqld.cnf.bak
```
* Agregar en ``` mysqld.cnf ```:
```
[mysqld]
secure-file-priv = ""
local-infile = 1 
```
Se recomienda restaurar la configuración inicial de ``` mysqld.cnf ``` al terminar todo. 

## Instrucciones
* Creación de un usuario y de la tabla base de datos ```grupos``` y de la tabla ```grupo4```
```
$ sudo mysql
mysql> CREATE USER 'usuariotabla'@'localhost' IDENTIFIED BY 'pass1234'; 
mysql> GRANT ALL PRIVILEGES ON *.* TO 'usuariotabla'@'localhost' WITH GRANT OPTION;

mysql> CREATE DATABASE grupos;
mysql> USE grupos;
mysql> CREATE TABLE grupo4 (id INT AUTO_INCREMENT PRIMARY KEY NOT NULL, unidad VARCHAR(50), nombre VARCHAR(255), apellidos VARCHAR(255), edad INT); 
```

* Para poder tener permisos para leer archivos con las instrucciones LOAD DATA LOCAL INFILE de MySQL
```
mysql> SET GLOBAL local_infile=1;
mysql> EXIT;
#Iniciar mysql
$ sudo mysql -u usuariotabla -p --local-infile=1 grupos
```

* Lectura del archivo .csv
```
mysql> USE grupos;
mysql> LOAD DATA LOCAL INFILE '/home/ivan/Documents/Proyectos_java/java_mysql/Capstone Project.csv' INTO TABLE grupo4 FIELDS TERMINATED BY ',' IGNORE 1 LINES (unidad, nombre, apellidos, edad);
```
* Ordenamiento usando consultas MySQL
```
SELECT * FROM grupo4 ORDER BY nombre ASC;
SELECT * FROM grupo4 ORDER BY nombre, apellidos ASC;
SELECT * FROM grupo4 ORDER BY edad ASC;
```

## Imágenes
* Consultas desde Java <br>
![java_orden_apellidonombre2](https://user-images.githubusercontent.com/87504488/141658667-f6819caf-2da1-42f4-bf54-1fb67ef68c7b.jpg)
![java_orden_edad2](https://user-images.githubusercontent.com/87504488/141658670-b7967bb2-8c61-47f7-a1b5-33631edd1564.jpg)

