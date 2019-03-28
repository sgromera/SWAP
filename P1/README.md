# Práctica 1

Hemos creado 2 máquinas virtuales, cada una con Ubuntu Server 16.04 con la imagen que se nos dio en clase. 

![Captura 1](https://github.com/sgromera/SWAP/blob/31359c8934c4b59cc830706ac4dcb9f86ef6cbc9/P1/5_VBox.png)

Una vez hecha la instalación (durante la cual se ha instalado LAMP y OpenSSH) se configura una nueva interfaz de red en cada máquina de tipo 'Internal Network'. Se configuran las máquinas como en la siguiente captura.

![Captura 2](https://github.com/sgromera/SWAP/blob/31359c8934c4b59cc830706ac4dcb9f86ef6cbc9/P1/1_Host.png)

Una máquina tiene IP 192.168.1.100 y la otra 192.168.1.101. Creamos un fichero HTML para comprobar la conexión entre ambas máquinas. A continuación probamos a recibirlo con curl.

![Captura 3](https://github.com/sgromera/SWAP/blob/31359c8934c4b59cc830706ac4dcb9f86ef6cbc9/P1/3_Host.png)

![Captura 4](https://github.com/sgromera/SWAP/blob/31359c8934c4b59cc830706ac4dcb9f86ef6cbc9/P1/4_client.png)

Ambas máquinas se ven.

Vamos a probar a hacer ssh para conectar ambas máquinas. (La conexión con ssh se ha hecho después de hacer la práctica 2, por eso no pide password)

![Conexión con ssh](https://raw.githubusercontent.com/sgromera/SWAP/master/P1/ssh_touch.png)

Comprobamos que se ha creado el archivo

![Comprobación ssh](https://raw.githubusercontent.com/sgromera/SWAP/master/P1/ssh_comprobacion.png)

Prácticas realizadas por:

José Luis Rojano Ramírez

Sergio Romera Guzmán
