1. Descarga la imagen 'ubuntu y comprueba que está en tu equipo

docker pull ubuntu

docker images

Esto nos mostrará la lista de imágenes de Docker en nuestro sistema,  deberiamos ver "ubuntu" en la lista.

2. Crea un contenedor sin ponerle nombre. ¿está arrancado? Obtén el nombre

docker run -d ubuntu sleep infinity
docker ps


El comando docker ps nos mostrará la lista de contenedores en ejecución. Deberiamos ver un contenedor sin nombre en la lista.

3. Crea un contenedor con el nombre 'ubu1'. ¿Como puedes acceder a él?

docker run -d --name ubu1 ubuntu sleep infinity

Para acceder al contenedor 'ubu1', usaremos el siguiente comando:

docker exec -it ubu1 bash

Esto nos abrirá una shell dentro del contenedor.

4. Comprueba que ip tiene y si puedes hacer un ping a google.com

Dentro del contenedor 'ubu1', ejecutamos estos comandos:

ip addr
ping google.com

5. Crea un contenedor con el nombre 'ubu2'. ¿Puedes hacer ping entre los contenedores?

docker run -d --name ubu2 ubuntu sleep infinity

Para hacer ping entre los contenedores 'ubu1' y 'ubu2', primero necesitamos obtener las direcciones IP de ambos contenedores y luego ejecutar el comando ping. Desde el host, puedes obtener la dirección IP de un contenedor de la siguiente manera:

docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' ubu1
docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' ubu2

Luego, desde 'ubu1' o 'ubu2', podemos hacer ping al otro contenedor utilizando su dirección IP.

6. Sal del terminal, ¿que ocurrió con el contenedor?

Si sales del terminal sin detener los contenedores, estos seguirán ejecutándose en segundo plano.

Para ver cuanto espacio en disco ocupan los contenedores, puedes utilizar el siguiente comando:

docker system df

7. ¿Cuanta memoria en el disco duro ocupaste? ¿Hay alguna herramienta de docker para calcularlo?

Ejecutamos el siguiente comando para obtener información sobre todos los contenedores en ejecución:

docker stats --all

8. ¿Cuanta RAM ocupan los contenedores? Crea cuantos contenedores necesites para calcularlo.

Esto te mostrará una lista de contenedores junto con estadísticas de uso de CPU, memoria y más.