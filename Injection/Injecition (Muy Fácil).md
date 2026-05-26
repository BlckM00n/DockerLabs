lo primero que hice fue escaneo general sobre la ip de la victima para ver que puertos que tiene abiertos.
![Texto](Pasted image 20250727223236.png)
Los parámetros utilizados son los siguiente:
-p-:	Escanea todos los 65535 puertos TCP, desde el 1 al 65535.
--open:	Muestra solo los puertos abiertos, omite los cerrados o filtrados.
-sT:	Realiza un TCP connect scan (conexión completa con el sistema operativo).
--min-rate 5000:	Envía al menos 5000 paquetes por segundo (acelera el escaneo, útil para ganar rapidez).
-vvv:	 Muestra salida muy detallada (modo muy verboso).
-n:	No realiza resolución DNS (no intenta convertir IP a nombre de dominio).
-Pn:	No hace ping previo, asume que el host está activo.
172.17.0.2: 	IP del objetivo que se quiere escanear.
-oG allPorts: Guarda los resultados en formato grepable en el archivo llamado allPorts.

con estos parámetros pude identificar que la victima tenia los puertos 22 y 80 abiertos los cuales pertenecen al los servicios de SSH y HTTP

Luego accedemos a la pagina web atreves donde nos encontramos con un panel de login. 
![[Pasted image 20250727223902.png]]
Gracias al nombre de la maquina puedo darme la idea de la técnica que debo utilizar la cual seria SQL Injection.
![[Pasted image 20250727224149.png]]
probamos el parámetro **admin' or 1=1-- -**" el cual sirve para Omitir la verificación de contraseña y logra un **inicio de sesión sin necesidad de conocer la clave**, si el backend no valida correctamente las entradas.
![[Pasted image 20250727224259.png]]
Gracias ah esto pude bypasearlo de manera exitosa y conseguí la contraseña del usuario Dylan. ahora con esto intentamos hacer una conexión atreves de SSH con este usuario y contraseña.
![[Pasted image 20250727224631.png]]Listo tengo conexión atreves de SSH ahora solo me quedaría hacer una escala de privilegios y listo.
![[Pasted image 20250727225332.png]]Hemos alcanzado el nivel de privilegios máximos en el sistema!
