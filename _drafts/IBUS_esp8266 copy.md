---
layout: post
title: PROTOCOLO IBUS
img: receptor.png
categories: esp8266 IOT Arduino
tags: esp8266 IOT Arduino
---  
<p>Con el objetivo de añadir un control remoto de radio control a futuros proyectos, analizaremos el protocolo de comunicación <b>IBUS</b> </p>
<p>Se usaran para las pruebas del protocolo la tarjesta NodeMCU_DECKIT_1_0, la cual incuye un módulo esp8266, ademas se usaran los receptorores de la marca  Flysky <b>FS-A8S 2.4G</b> y el  <b>FS-IA6B</b> con su respectivo control Flysky FS-i6X 2.4GHz de 10 canales </p>
 <figure class="figure col-md-6">
    <img class="figure-img img-fluid rounded" src="{{site.baseurl}}/images/receptor.png">
    <figcaption class="figure-caption text-center">FS-IA6B</figcaption>
 </figure> 
 <figure class="figure col-md-6">
    <img class="figure-img img-fluid rounded" src="{{site.baseurl}}/images/receptorRF.jpg">
    <figcaption class="figure-caption text-center">FS-A8S 2.4G 8CH</figcaption>
 </figure>
  <figure class="figure col-md-6">
    <img class="figure-img img-fluid rounded" src="{{site.baseurl}}/images/NodeMCU_DEVKIT_1_0.jpg">
    <figcaption class="figure-caption text-center">NodeMCU_DEVKIT_1_0</figcaption>
 </figure> 
 <figure class="figure col-md-6">
    <img class="figure-img img-fluid rounded" src="{{site.baseurl}}/images/radioFlysky.jpg">
    <figcaption class="figure-caption text-center">FS-i6X 2.4GHz</figcaption>
 </figure> 

 

<p>IBUS es un protocolo de comunicación  serial desarrollado por la compañía  Flysly.</p>
<p>Algunas de las propiedades del protocolo Ibus son las siguientes: </p>
<ul>
<li><p>Protocolo de comunicación bidireccional.</p></li>
<li><p>Cada mensaje es enviado cada 7.7 milisegundos aproximadamente</p>
 <figure class="figure">
    <img class="img-responsive img-rounded img-fluid" src="{{site.baseurl}}/images/timetomessage.png">
    <figcaption class="figure-caption text-center">Captura de datos cada 7.7 milisegundos</figcaption>
</figure>
</li>
<li>
 <p>Los datos son trasmitidos en forma serial con una velocidad de trasmisión de unos 115200 baudios, con 8 bits de datos sin paridad y 1 bit de parada.</p>
  <figure class="figure">
    <img class="img-responsive img-rounded img-fluid" src="{{site.baseurl}}/images/serialConfig.png">
    <figcaption class="figure-caption text-center">Configuración protocolo serial</figcaption>
 </figure>
</li>
<li>
 <p>El primer byte es un 0x20 seguido de un segundo byte 0x40 seguido de  14 pares de bytes con la información de cada uno de los canales, el valor de cada canal esta compuesto por 2 bytes siendo el menos significativo el que se recibe primero es decir formato little endian.</p>
 formato de la trama:
{% highlight CPP %}
   0x20 0x40 CH0 CH1 CH2 CH3 CH4 CH5 CH6 CH7 CH8 CH9 CH10 CH11 CH12 CH13 SUM 
{% endhighlight %}
  <figure class="figure">
    <img class="img-responsive img-rounded img-fluid" src="{{site.baseurl}}/images/formatFrame.png">
    <figcaption class="figure-caption text-center">Captura frame protocolo IBUS</figcaption>
 </figure>
</li>
</ul>

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