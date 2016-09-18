#Trabajo SWAP: Configuración del cortafuegos de la granja web

Para configurar el cortafuegos de la máquina vamos a usar el programa UFW, que viene por defecto intalado. Se reaizara sobre una máquina con nginx configurada para que redirija el trafico al balanceador de la granja web.

En primer lugar utilizamos el comando

sudo ufw status

Para comprobar si esta activo o no UFW. Si esta desactivado utilizamos el comando 

sudo ufw enable

![Activando UFW](Imagenes/imagen1.PNG) 

Con la herramienta nmap podemos comproobar que puertos tiene abiertos una máquina. A modo de ejemplo, vamos a ejecutar nmap en una de las maquinas finales para ver que puertos tiene abiertos. En este caso solo comprobamos los 1000 (comando -p) primeros puertos tcp (opcion por defecto)

![nmap Maquina 1](Imagenes/imagen2.PNG) 

Y ahora a la máquina CORTAFUEGOS

![nmap cortafuegos](Imagenes/imagen3.PNG) 

Como vemos no tenemos ningún puerto abierto.

Para dar acceso solamente a comunicaciones http y https abrimos los puertos del cortafuegos 80 y 443 con las ordenes

sudo ufw allow 80/tcp
sudo ufw allow 443/tcp

Y escneamos, obteniendo los puertos 80 y 443

![nmap Cortafuegos 2](Imagenes/imagen4.PNG) 

Configuramos gninx para que apunte al balanceador y reiniciamos el servicio

![Configurando cortafuegos](Imagenes/imagen5.PNG) 

Ahora hacemos las peticiones a la maquina firewall y vemos como se realizan las peticiones correctamente

![Peticiones](Imagenes/imagen6.PNG) 