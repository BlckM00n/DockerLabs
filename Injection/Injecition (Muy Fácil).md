Lo primero que hice fue realizar un escaneo general sobre la IP de la víctima para identificar qué puertos tenía abiertos.

![Escaneo Nmap](nmap.png)

Los parámetros utilizados son los siguientes:

- `-p-`: Escanea todos los 65535 puertos TCP, desde el 1 al 65535.
- `--open`: Muestra solo los puertos abiertos, omitiendo los cerrados o filtrados.
- `-sT`: Realiza un TCP Connect Scan (conexión completa utilizando el sistema operativo).
- `--min-rate 5000`: Envía al menos 5000 paquetes por segundo para acelerar el escaneo.
- `-vvv`: Muestra una salida muy detallada (modo verbose).
- `-n`: No realiza resolución DNS.
- `-Pn`: Asume que el host está activo sin realizar ping previo.
- `172.17.0.2`: IP del objetivo.
- `-oG allPorts`: Guarda los resultados en formato grepable dentro del archivo `allPorts`.

Con estos parámetros pude identificar que la víctima tenía abiertos los puertos 22 y 80, correspondientes a los servicios SSH y HTTP.

Luego accedemos a la página web, donde nos encontramos con un panel de login.

![Panel Login](Login.png)

Gracias al nombre de la máquina pude inferir que la técnica a utilizar sería SQL Injection.

![SQL Injection](SQLi.png)

Probamos el parámetro:

"admin' or 1=1-- -"

Este payload permite omitir la verificación de contraseña y realizar un inicio de sesión sin necesidad de conocer la clave, siempre y cuando el backend no valide correctamente las entradas del usuario.

![Bypass Login](SQLR.png)

Gracias a esto pude bypassear el login de manera exitosa y obtener la contraseña del usuario Dylan.

Ahora, utilizando estas credenciales, intentamos realizar una conexión mediante SSH con el usuario y contraseña obtenidos.

![Conexion SSH](SSH.png)

Listo, ya tenemos acceso al sistema mediante SSH. Ahora solamente quedaría realizar una escalada de privilegios para obtener acceso total al sistema.

![Escalada de Privilegios](Root.png)

¡Hemos alcanzado el máximo nivel de privilegios en el sistema!
