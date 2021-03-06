---
layout: post
title: Instalación Broker MQTT emqx
img: emqx_head.png
categories: IOT
tags: IOT Docker
---
### ¿Qué es EMQX?

EMQX es un broker MQTT de código abierto altamente escalable y permite la creación de un cluster con múltiples nodos lo que facilita el manejo de miles de conexiones, EMQX permite su gestión a través de un dashboard muy completo e integra varios plugins que facilitan el manejo de usuarios y reglas para administrar los permisos de cada uno.


### Instalación

Para la instalación del broker se puede sar Docker corriendo un contenedor con una instancia de EMQX sobre una Raspberry Pi 3

#### Instalación docker

Con los siguientes comandos se instala los paquetes docker.io.
{% highlight sh %}
sudo apt-get install docker.io
{% endhighlight %}

#### Instalación del contenedor EMQX

{% highlight sh %}
docker run -d --name emqx -p 18083:18083 -p 1883:1883 -p 8083:8083 -p 8084:8084 -e EMQX_ALLOW_ANONYMOUS=false emqx/emqx:latest
{% endhighlight %}

En el anterior comando no se permite la conexión de usuarios anónimos, en caso de querer permitirlos se cambia la variable de entorno **EMQX_ALLOW_ANONYMOUS** a True.

Luego de que termine la descarga de la imagen e inicie el contenedor se puede acceder al broker EMQX mediante el navegador en la dirección **http://ip_raspberry:18083** 

Las credenciales por defecto son username = **admin** y password = **public**, luego de acceder se pueden cambiar  en la pestaña **Users**

{% include imagen.html id='emqx/emqx_1.png' %}

Se procede a iniciar el plugin **EMQ X Authentication with Username and Password** que nos permite manejar los usuarios que tienen permiso para conectarse al broker, debido a que se configuró el broker para no permitir usuarios anónimos.

{% include imagen.html id='emqx/plugin_usuarios.png' %}

En esta pestaña se crea un usuario de pruebas con clic en el botón **Manage** e ingresando el username y password.

{% include imagen.html id='emqx/emqx_user.png' %}

Por ultimo probamos que nos podamos conectar al broker mediante el usuario creado, para esto usamos una herramienta que nos provee EMQX la cual encontramos en la pestaña **tools** y en **Websocket**  e ingresamos  en Username el usuario creado y la contraseña y ya solo queda hacer click en conectar como se muestra en la siguiente imagen.

{% include imagen.html id='emqx/websocket_conn.png' %}

EMQX es un broker muy completo, para mas información es recomendado leer la documentación donde se destaca todas las características que esta herramienta nos ofrece.


## Referencias

<a href="https://docs.emqx.io/en/broker/latest/" target="_blank"><i class="fa fa-link" aria-hidden="true"></i> Documentación broker EMQX</a>

<a href="https://hub.docker.com/r/emqx/emqx" target="_blank"><i class="fa fa-link" aria-hidden="true"></i>https://hub.docker.com/r/emqx/emqx</a>
