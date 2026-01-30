# Configuración de FTP seguro (FTPS)

## Generación de un certificado TLS
1. Vamos a FileZilla Server Administration - Server - Configure - Administration - Connection security y ponemos "Use a self-signed X.509 certificate" en "TLS credentials" y generamos un certificado nuevo el cual rellenamos con la información oportuna.
![](https://github.com/JavierMoralesSimon/filezillaFTPS/blob/main/Capturas/1.png)

## Configuración de FileZilla Server para FTPS explícito.
1. En FileZilla Server Administration - Server - Server Listeners, ponemos un listener en el puerto 21 y marcamos "Require explicit FTP over TLS".
![](https://github.com/JavierMoralesSimon/filezillaFTPS/blob/main/Capturas/2.1.png)
2. Vamos a FTP and FTP over TLS (FTPS) - Passive mode y definimos un rango de puertos como por ejemplo 50000-50100.
![](https://github.com/JavierMoralesSimon/filezillaFTPS/blob/main/Capturas/2.2.png)
3. Abrir los puertos puestos antes y el 21 en el firewall de Ubuntu mediante los comandos `sudo ufw allow 21/tcp` y `sudo ufw allow 50000:50100/tcp`.
![](https://github.com/JavierMoralesSimon/filezillaFTPS/blob/main/Capturas/2.3.png)

## Uso de conexión segura para usuarios
Ir a FileZilla Server Administration - Server - Configure - Users y en el usuario elegido vamos a Protocol polices - FTPS (FTP over TLS) authentication y marcamos "Enabled override group polices".
![](https://github.com/JavierMoralesSimon/filezillaFTPS/blob/main/Capturas/3.png)

## Validación
1. Abrir FileZilla Client - Gestor de Sitios.
2. Crear una nueva conexión.
3. En General seleccionar el protocolo "FTP - Protocolo de transferencia de archivos", de cifrado "Requerir FTP explícito sobre TLS", modo de acceso normal, la IP deseada, el usuario y su contraseña.
![](https://github.com/JavierMoralesSimon/filezillaFTPS/blob/main/Capturas/4.1.png)
4. En "Opciones de transferencia" poner pasivo.
![](https://github.com/JavierMoralesSimon/filezillaFTPS/blob/main/Capturas/4.2.png)
5. Nos conectamos.
![](https://github.com/JavierMoralesSimon/filezillaFTPS/blob/main/Capturas/4.3.png)
6. Si damos al candado de abajo, nos salen los detalles del certificado.
![](https://github.com/JavierMoralesSimon/filezillaFTPS/blob/main/Capturas/4.4.png)

## Prueba de fuego
1. Desconectarse.
![](https://github.com/JavierMoralesSimon/filezillaFTPS/blob/main/Capturas/5.1.png)
2. Cambiar la configuración del sitio en el cliente a "Usar solo FTP plano (inseguro)".
![](https://github.com/JavierMoralesSimon/filezillaFTPS/blob/main/Capturas/5.2.png)
3. Intento de conexión que da error.
![](https://github.com/JavierMoralesSimon/filezillaFTPS/blob/main/Capturas/5.3.png)
