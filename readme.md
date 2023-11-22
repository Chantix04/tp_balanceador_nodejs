## Tp3 -- Balanceador de Carga con sitios nodejs || También sirve para el tp4 -- Crear nuestras propias imágenes con dockerfile, ya que tiene archivos dockerfile donde creamos imagenes

1)- Creo una nueva red con este comando: docker network create rednode

2)- Creo 3 carpetas, dos son para el front y uno para el balanceador. Dentro de cada carpeta aplicacion-node estara un servidor basico que muestre un mensaje

3)- Este es el comando que utilice para crear el contenedor, es importante poner el puerto de la misma direccion de port de node que esta en el vscode

docker run --name nodewebuno -p 8090:81 --network rednode -v C:\Users\gstnr\Desktop\php\nodejs\aplicacion-node:/usr/src/app -w /usr/src/app -d node:14 bash -c "node index.js" --> Me posiciono en la carpeta de aplicacion-node 

docker run --name nodewebdos -p 8089:81 --network rednode -v C:\Users\gstnr\Desktop\php\nodejs\aplicacion-node2:/usr/src/app -w /usr/src/app -d node:14 bash -c "node index.js"--> Me posiciono en la carpeta de aplicacion-node 

4)- Creo ahora mi balanceador de carga con haproxy vincuando a la red dnd estan los dos servidores node

docker run -d --name haproxynode --network rednode -p 8095:81 -v C:\Users\gstnr\Desktop\php\nodejs\balanceador/haproxy.cfg:/usr/local/etc/haproxy/haproxy.cfg:ro haproxy:latest  
