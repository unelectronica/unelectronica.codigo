---
layout: post
title: Hola Mundo Stm32
img: stm32.png
categories: STM32
tags: STM32
---
Este será el primer proyecto usando una tarjeta de desarrollo basada en el microcontrolador **ARM Cortex M3 STM32F103C8T6** de 32 bits de la empresa STMicroelectronics , el cual cuenta con las siguientes características:

* Empaquetado: LQFP
* Número de pines: 48
* Núcleo: 32-bit ARM Cortex M3.
* Memoria Flash: 64 Kilobytes
* Memoria SRAM: 20 Kilobytes
* 8MHz de reloj de placa.
* 72 MHz de frecuencia de operación.
* 1 reloj de tiempo real (RTC)
* 26 entradas y salidas digitales.
* Interrupciones en todos los pines I/O.
* ADC: 2 ADC de 12-bit, o entradas analógicas. 
* 7 temporizadores de propósito general de 16 bits.
* 2 puertos I2C.
* 2 puertos SPI.
* 3 puertos RS232 USUARTs.
* 1 puerto CAN.
* Micro USB para alimentación y comunicación de la placa.
* Soporta DEBUG por JTAG y SWD
* Tensión de funcionamiento entre 2 Vcc y 3.6 Vcc.

El microcontrolador STM32F103C8T6 permite cargar el firmware en la memoria SRAM como en la memoria FLASH, para lo cual cuenta con un pin llamado BOOT0 y dependiendo si está a gnd o vcc el firmware se carga en una memoria o en la otra, la tarjeta de desarrollo cuenta con dos Jumpers para esta función.

<table class="table table-bordered table-hover">
  <thead>
    <tr>
      <th scope="col">BOOT1</th>
      <th scope="col">BOOT0</th>
      <th scope="col">MODO</th>
    </tr>
  </thead>
  <tbody>
    <tr>
     <td>x</td><td>0</td><td>FLASH</td>
    </tr>
    <tr>
     <td>0</td><td>1</td><td>RAM</td>
    </tr>
    <tr>
     <td>1</td><td>1</td><td>Ext. SRAM</td>
    </tr>
  </tbody>

</table>

<figure class="figure text-center">
  <img src= "{{site.baseurl}}/images/BOOT-SELECTOR.png" class="figure-img img-fluid rounded">
  <figcaption class="figure-caption">Jumpers selección de Boot.</figcaption>
</figure>
---
La placa puede ser programada por dos métodos, mediante un adaptador USB-SERIE o con el adaptador ST-LINK este último es un programador específico para los microcontroladores de la familia STM32 y STM8 el cual permite realizar procesos de depuración.

   <figure class="figure col-md-6">
    <img class="img-responsive rounded img-fluid" src="{{site.baseurl}}/images/st-link-v2.jpg">
    <figcaption class="figure-caption text-center">Adaptador ST-LINK.</figcaption>
  </figure>

  <figure class="figure col-md-6">
    <img class="img-responsive rounded img-fluid" src="{{site.baseurl}}/images/conversor-usb-a-serie.jpg">
    <figcaption class="figure-caption text-center">Conversor USB a serie.</figcaption>
  </figure>

 <figure class="figure">
    <img class="img-responsive rounded img-fluid" src="{{site.baseurl}}/images/STM32F103C8T6_PINOUT.jpg">
    <figcaption class="figure-caption text-center">Pinout tarjeta de desarrollo</figcaption>
  </figure>
  Programa de prueba, la tarjeta cuenta con un led conectado al pin PC13 

{% highlight CPP %}

void setup() {
    pinMode(PC13, OUTPUT);
}

// the loop function runs over and over again forever
void loop() {
  digitalWrite(PC13, HIGH); 
  delay(1000);             
  digitalWrite(PC13, LOW);   
  delay(1000);           
}
{% endhighlight %}


<h3>Referencias</h3>
<ul>
  <li> <a href="https://github.com/esp8266/Arduino" target="_blank"><i class="fa fa-github" aria-hidden="true"></i> ESP8266 IDE Arduino</a></li>
  <li> <a href="https://github.com/nodemcu/nodemcu-devkit-v1.0" target="_blank"><i class="fa fa-github" aria-hidden="true"></i> nodemcu-devkit-v1.0</a></li>

</ul>
<h3>Código</h3>
<ul>
  <li><a href="https://github.com/unelectronica/SocketConnect" target="_blank"><i class="fa fa-github" aria-hidden="true"></i> SocketConnect</a></li>
  <li><a href="https://github.com/unelectronica/notas-microcontroladores/tree/master/ESP8266/ledWifi/ledWifi.ino" target="_blank"><i class="fa fa-github" aria-hidden="true"></i> Led WiFi</a></li>
</ul>


