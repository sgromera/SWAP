# Práctica 5:

En esta práctica trataremos de replicar bases de datos entre las distintas máquinas que forman nuestra granja web, de forma maestro-esclavo, dode los cambios realizados en la base de datos maestro se reflejen en el esclavo.

Lo primero que haremos será crear nuestra Base de datos e insertar unos datos y replicarlos en la otra máquina. Para utilizar MySql utilizamos el siguiente comando:

*mysql -u root -p*

Creamos la base de datos e introducimos los datos

![Imagen1](https://raw.githubusercontent.com/sgromera/SWAP/master/P5/sql-data.png)

Para poder replicar la base de datos podemos exportar los datos con *mysqldump*. Utilizamos el siguiente comando:

*mysqldump contactos -u root -p > ./contactos.sql*

![Imagen2](https://raw.githubusercontent.com/sgromera/SWAP/master/P5/mysqldump.png)

Para enviar el archivo entre máquinas, en este caso, usaremos *sftp*.

![Imagen3](https://raw.githubusercontent.com/sgromera/SWAP/master/P5/sftp.png)

Ahora trataremos de replicar la base de datos creada en otra máquina que funcionará como máquina esclava. Modificamos el archivo /etc/mysql/mysql.conf.d/mysql.cnf tanto en la BD maestra como en la esclava.Creamos el usuario esclavo en la base de datos maestro.

![Imagen4](https://raw.githubusercontent.com/sgromera/SWAP/master/P5/crea_esclavo.png)

Mediante el comando *SHOW MASTER STATUS* podemos ver los datos necesarios para enlazar la base de datos esclava

![Imagen5](https://raw.githubusercontent.com/sgromera/SWAP/master/P5/show_master_status.png)

En la BD esclava ejecutamos el comando *CHANGE MASTER TO MASTER_HOST='192.168.1.100' MASTER_USER='esclavo1', MASTER_PASSWORD='esclavo1', MASTER_LOG_FILE='mysql-bin.000003', MASTER_LOG_POS=2080, MASTER_PORT=3306*

Ejecutamos *START SLAVE;* en la BD esclava y *SHOW SLAVE STATUS\G*

![Imagen6](https://raw.githubusercontent.com/sgromera/SWAP/master/P5/show_slave_status.png)

Comprobamos que no hay fallo, mirando en el campo Seconds_Behind_Master que no sea NULL. Ya que no hay fallo vamos a realizar un cambio en la máquina maestra para comprobar el funcionamiento.

Realizamos los cambios en el maestro:

![Imagen7](https://raw.githubusercontent.com/sgromera/SWAP/master/P5/cambios_maestro.png)

Comprobamos en el esclavo:

![Imagen8](https://raw.githubusercontent.com/sgromera/SWAP/master/P5/cambios_esclavo.png)

Prácticas realizadas por:
José Luis Rojano Ramírez
Sergio Romera Guzmán
