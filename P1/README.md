# PRÁCTICA 1: PRESENTACIÓN Y PREPARACIÓN DE HERRAMIENTAS

Esta práctica consistirá en preparar las herramientas que se utilizarán en las siguientes prácticas.
Las herramientas son Openssh, Servidor LAMP y cURL.

Para instalar Openssh y el Servidor LAMP se puede hacer con `tasksel` y elegir las opciones `OpenSSH server` y `LAMP server`.

![img]()


![img]()


## Crear tarjeta de Red

En este caso utilizaremos una tarjeta de red Host-Only.
Para instalarla hay que ir a `Herramientas globales`->`Crear`.
A esta tarjeta de red se le hará que su dirección IP sea estática y que nosotros decidamos cuál sería.
Para ello seleccionamos en la parte inferior de la pantalla `Servidor DHCP`->`Habilitar servidor`, y en el campo `Dirección del servidor` dejamos la que está por defecto, el campo `Máscara del servidor` también se queda el que está por defecto y los dos siguientes son el rango de direcciones en el que estará la dirección del servidor.

-----------------------------------------------

![img]()

-----------------------------------------------

![img]()


Lo próximo que hay que hacer es configurar la red y para ello tendremos que arrancar la máquina.

A continuación pondremos el comando:

    `sudo vi /etc/network/interfaces`

Y añadiremos al final del fichero

Nueva red
auto enp0s8
iface enp0s8 inet static

address 192.168.56.xxx
mask 255.255.255.0
gateway 192.168.56.1

![img]()

Las x's son un número cualquiera siempre y cuando se encuentre en el intervalo que hemos creado en `Herramientas globales`->`Servidor DHCP` en los dos últimos campos.
De esta forma la dirección IP de nuestro servidor será estática, es decir, no cambiará cada vez quela arranquemos.

Para comprobarlo lo que debemos de hacer es tener las dos máquinas encendidas y realizar `ping` con la direccción IP de la otra máquina

    `ping <dirección IP de la otra máquina>`

![img]()


![img]()


## Conexión ssh

Al haber descargado ya el paquete de OpenSSH lo único que tenemos que hacer es:

    `ssh <nombre Usuario>@<dirección IP de la otra máquina>`

A continuación tenemos que poner la contraseña del usuario al que nos queremos conectar y finalmente estaríamos conectados a la otra máquina.

![img]()


![img]()


## Conexión cURL

Antes de todo tenemos que descargar la herramienta, si no está ya instalada en las dos máquinas, con:

    `sudo apt-get install curl`

Además de tener las herramientas del servidor LAMP: apache, mySQL y php.

A continuación, teniendo esto ya hecho, vamos a utilizarlo para comprobar que tenemos conexión entre las dos máquinas mediante http con `curl http://<IP del servidor>/<directorio, si es necesario>/<archivo HTML que queremos obtener>`.

![img]()


![img]()