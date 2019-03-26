---
layout: post
title: PROTOCOLO IBUS
img: receptor.png
categories: esp8266 IOT, Arduino
tags: esp8266 IOT Arduino
---  
<p>Con el objetivo de añadir un control remoto a futuros proyectos, analizaremos el protocolo de comunicación <b>IBUS</b> </p>
<p>Usaremos la tarjeta NodeMCU_DEVKIT_1_0 y por medio del protocolo MQTT controlaremos un led que viene en esta tarjeta de desarrollo.</p>

<p>IBUS es un protocolo de comunicación  serial desarrollado por la compañía  Flysly. Es un protocolo de comunicación bidireccional, los datos son trasmitidos en forma serial con una velocidad de trasmisión de unos 115200 baudios, con 8 bits de datos sin paridad y 1 bit de parada, cada mensaje es enviado cada 7 milisegundos, el primer byte es un 0x20 seguido de un segundo byte 0x40 seguido de  14 pares de bytes con la información de cada uno de los canales, el valor de cada canal esta compuesto por 2 bytes siendo el menos significativo el que se recibe primero es decir formato little endian</p>
formato de la trama:
{% highlight CPP %}
   0x20 0x40 CH0 CH1 CH2 CH3 CH4 CH5 CH6 CH7 CH8 CH9 CH10 CH11 CH12 CH13 SUM 
{% endhighlight %}
Según los canales que estén en uso por el transmisor se llenan los primeros valores, los canales sin uso quedan con el valor 0x05DC, los dos últimos bytes de la trama son dedicados para el checksum el cual inicia con el valor OxFFFF y se van restando los valores de cada canal.


 <figure class="figure">
    <img class="img-responsive img-rounded img-fluid" src="{{site.baseurl}}/images/receptorPins.png">
 </figure>

<h3>Referencias</h3>
<ul>
  <li> <a href="http://blog.dsp.id.au/posts/2017/10/22/flysky-ibus-protocol/" target="_blank">http://blog.dsp.id.au/posts/2017/10/22/flysky-ibus-protocol/</a></li>
  <li> <a href="https://basejunction.wordpress.com/2015/08/23/en-flysky-i6-14-channels-part1/" target="_blank">https://basejunction.wordpress.com/2015/08/23/en-flysky-i6-14-channels-part1/</a></li>
  <li>
  <a href="https://github.com/33d/ibus-library/blob/master/ibus.h" target ="_blank">https://github.com/33d/ibus-library/blob/master/ibus.h</a>
  </li>
    <li>
  <a href="https://github.com/aanon4/FlySkyIBus" target ="_blank">https://github.com/aanon4/FlySkyIBus</a>
  </li>
</ul>