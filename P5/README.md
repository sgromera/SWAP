# Práctica 5:

En esta práctica trataremos de replicar bases de datos entre las distintas máquinas que forman nuestra granja web, de forma maestro-esclavo, dode los cambios realizados en la base de datos maestro se reflejen en el esclavo.

Lo primero que haremos será crear nuestra Base de datos e insertar unos datos y replicarlos en la otra máquina. Para utilizar MySql utilizamos el siguiente comando:

*mysql -u root -p*

Creamos la base de datos e introducimos los datos

[!Imagen1]()

Para poder replicar la base de datos podemos exportar los datos con *mysqldump*. Utilizamos el siguiente comando:

*mysqldump contactos -u root -p > ./contactos.sql*

[!Imagen2]()

Para enviar el archivo entre máquinas, en este caso, usaremos *sftp*.

[!Imagen3]()

Ahora trataremos de replicar la base de datos creada en otra máquina que funcionará como máquina esclava. Primero creamos el usuario esclavo en la base de datos maestro.

[!Imagen4]()
