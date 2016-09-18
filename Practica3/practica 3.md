#Práctica 3: Balanceo de carga

El objetivo de esta practica práctica, es configurar una red entre varias máquinas de forma que tengamos un balanceador que reparta la carga entre varios servidores finales.

#Balanceo con nginx

Una vez tenemos instalados nginx, debemos modificar su configuración, ya que la que trae por defecto se corresponde a la funcionalidad de un servidor web.

Para ello modificamos el fichero /etc/nginx/conf.d/default.conf dejandolo de la siguiente manera:

![Configurando nginx](Imagenes/imagen1.PNG) 

Y despues reiniciamos el servicio nginx con el comando

service nginx restart

Y comprobamos con la orden curl el balanceo con nginx (round-robin en este caso)

![Round-Robin nginx](Imagenes/imagen2.PNG) 

Para que el balanceo de carga sea ponderado, deberemos añadir el modificador "weight" para modificar la carga de tráfico que recibe cada servidor

![Ponderado configuracion nginx](Imagenes/imagen3.PNG) 

En este caso la máquina 1 tiene el doble de capacidad que la máquina 2. Lo probamos con el comando curl

![Ponderado nginx](Imagenes/imagen4.PNG) 

#Balanceo con haproxy

Una vez instalado haproxy con apt-get, modificamos el fichero de configuración (/etc/haproxy/haproxy.conf) de la siguiente manera.

![CConfigurar haproxy](Imagenes/imagen5.PNG) 

Lanzamos el servicio haproxy con el comando

/usr/sbin/haproxy -f /etc/haproxy/haproxy.cfg

Y hacemos las peticiones a la máquina

![Round-Robin Haproxy](Imagenes/imagen6.PNG) 

Y para darle mas peso a la máquina 1 modificamos el archivo de configuración:

![Configuracion ponderada](Imagenes/imagen7.PNG) 

Y comprobamos que funciona

![Ponderada Haproxy](Imagenes/imagen8.PNG) 

