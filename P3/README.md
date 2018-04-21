#Mario Chaves Caballero
#Juan Carlos Quesada Hermoso

#Práctica 3: Balanceo de Carga

##Crear máquina balanceadora

Se instala **Ubuntu-Server16.08** con todos los valores por defecto en una nueva máquina para que esta sea nuestro balanceador. No se instala ningún paquete adicional y así ahorramos memoria, y nos aseguramos que no hay ningún software que se apodere del puerto 80 ya que es el pueto por el que se recibirán las peticiones **HTTP**.

Además, hemos creado una tarjeta de red host-only con la dirección IP estática `192.168.56.103`.

##Instalar nginx

Los comandos recomendados para la instalación de **nginx** por parte del guión son:

    `sudo apt-get update && sudo apt-get dist-upgrade && sudo apt-get autoremove`
    
    La cual sirve para actualizar el sistema y eliminar archivos sin utilidades.

![img]()

    `sudo apt-get install nginx`

    Con este comando se instala el servidor web **nginx**.

![img]()

`sudo systemctl start nginx`

    Con este comando se inicia el servidor **nginx**.

![img]()


------------------------------------------------------------------------------------------

##Configurar nginx como balanceador

Para confifurar nginx como balanceador tenemos que cambiar el contenido del fichero `/etc/nginx/conf.d/default.conf` o crearlo. Si el fichero ya existe tenemos que eliminar todo su contenido y cambiarlo por:


![img]()


A continuación reiniciamos **nginx** para que la configuración se guarde.

Luego hemos comprobado si la configuración funciona correctamente conectando con las máquinas finales mediante cURL:

cURL desde balanceador a máquina1:

![img]()

cURL desde balanceador a máquina2:

![img]()

En nuestro caso no hemos puesto peso a ninguna máquina ya que las dos tienen las mismas capacidades (son clonadas), hemos hecho que la carga que viene desde la misma dirección IP la gestione el mismo servidor final con `ip_hash` y hemos puesto que durate 5 segundos solo se tenga que hacer una sola conexión por la que llegarán las peticiones **HTTP** con `keepalive 5`, en vez de crear una conexión por petición.



------------------------------------------------------------------------------------------

##Benchmark en nginx

Primero tenemos que crear otra máquina de la misma forma como hemos creado la máquina balanceador, solo que ésta vez hemos instalado un servidor LAMP para poder utilizar un Apache Benchmark (ab).

La orden que hemos utilizado ha sido `ab -n 200000000 -c 50 http://192.168.56.103/index.html`, y como resultado ha sido este:

![img]()





