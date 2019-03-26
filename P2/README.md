# Práctica 2

En esta práctica trataremos de hacer que las dos máquinas que creamos en la práctica 1 estén sincronizadas, de forma que uno de los equipos hará de equipo principal y el otro de secundario. El equipo secundario tratará de estar al día con los archivos del principal, comprobando regularmente los cambios producidos en el otro equipo.

La herramienta que utilizaremos para la sincronización entre los equipos es **rsync**, que debemos instalar.

*sudo apt install rsync*

![Instalación rsync](https://raw.githubusercontent.com/sgromera/SWAP/master/P2/1_install_rsync.png)

Una vez hemos instalado rsync en ambas máquinas, vamos a realizar una prueba. Primero, en la máquina principal indicamos la carpeta de la cual el usuario será dueño.

*sudo chown {usuario}:{usuario} -R /var/www*

![Máquina principal](https://raw.githubusercontent.com/sgromera/SWAP/master/P2/2_maquina_due%C3%B1a.png)

Ahora podremos utilizar rsync con ssh para sincronizar la carpeta de la máquina principal (host) con la máquina secundaria. Para ello, utilizamos el comando con la siguiente sintaxis:

*rsync -avz -e ssh {host}:{directorio_host} {directorio_local}*

![Prueba de sincronización](https://raw.githubusercontent.com/sgromera/SWAP/master/P2/3_rsync_prueba.png)

El siguiente paso sería automatizar este proceso para que la máquina secundaria regularmente sincronizase estos directorios. Para hacer esto vamos a usar **crontab**, con el cual se pueden programar procesos daemon que se ejecuten en segundo plano con la regularidad que se indique.

En nuestro caso, vamos a tratar de crear un proceso que se ejecute **cada hora** que sincronice los directorios /var/wwww. Lo primero que haremos es crear una clave pública en la máquina secundaria. La necesitamos para poder realizar la conexión ssh sin necesidad de introducir la password del usuario y, por tanto, que el proceso se ejecute solo.

*ssh-keygen -b 4096 -t rsa*

![Generando clave pública](https://raw.githubusercontent.com/sgromera/SWAP/master/P2/4_keygen.png)

Una vez generamos nuestra clave pública, debemos llevarla a la máquina principal, en el directorio *~/.ssh/authorized_keys* . Esto se puede hacer de forma sencilla con el comando:

*ssh-copy-id {host}*

![Llevando la clave a la máquina principal](https://raw.githubusercontent.com/sgromera/SWAP/master/P2/5_autorizado.png)

Ahora ya podremos conectarnos a la máquina principal via ssh sin necesidad de introducir contraseña. Es momento de programar nuestra tarea en **crontab**. Para eso tenemos dos posibilidades: modificar el archivo /etc/crontab en modo superusuario; usar el comando *sudo crontab -e* y añadir la línea con nuestro comando.

Nosotros hemos decidido modificar el archivo de crontab mediante nano

*sudo nano /etc/crontab*

![Programando crontab](https://raw.githubusercontent.com/sgromera/SWAP/master/P2/6_crontab.png)

De izquierda a derecha vemos:
  - minutos: hemos definido '00' para que cada hora en punto se ejecute
  - horas: usamos '*' para indicar todas las horas
  - día del mes: usamos '*' para indicar todos los días del mes
  - día de la semana: usamos '*' para indicar todos los días de la semana
  - user: usamos el usuario 'sgromera2' ya que es con el que hemos definido la clave pública
  - comando: este es el comando que hemos descrito antes, usado para sincronizar los directorios
  
Práctica realizada por:

  José Luis Rojano Ramírez
  Sergio Romera Guzmán
