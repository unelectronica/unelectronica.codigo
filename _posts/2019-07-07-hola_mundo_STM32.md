---
layout: post
title: Primeros Pasos con los Stm32
img: STM32/stm32.png
categories: STM32
tags: STM32
---

Este será el primer proyecto usando una tarjeta de desarrollo basada en el microcontrolador **STM32F103C8T6** de 32 bits de la empresa STMicroelectronics, el cual posee un núcleo **ARM Cortex-M3**.

El microcontrolador **STM32F101C8T6** cuenta con las siguientes características:

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
* ADC: 2 ADC de 12-bit, 10 entradas analógicas. 
* 7 temporizadores de propósito general de 16 bits.
* 2 puertos I2C.
* 2 puertos SPI.
* 3 puertos RS232 USUARTs.
* 1 puerto CAN.
* Micro USB 2.0 (12 Mbit/s) para alimentación y comunicación de la placa.
* Soporta DEBUG por JTAG y SWD
* Tensión de funcionamiento entre 2 Vcc y 3.6 Vcc.
* una unidad de calculo CRC (cyclic redundancy check).

Este microcontrolador permite cargar el firmware en la memoria SRAM como en la memoria FLASH, para lo cual cuenta con un pin llamado BOOT0 y dependiendo si está a gnd o vcc el firmware se carga en una memoria o en la otra, la tarjeta de desarrollo cuenta con dos Jumpers para esta función.

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
  <img src= "{{site.baseurl}}/images/STM32/BOOT-SELECTOR.png" class="figure-img img-fluid rounded">
  <figcaption class="figure-caption">Jumpers selección de Boot.</figcaption>
</figure>
---
La placa puede ser programada por dos métodos, mediante un adaptador USB-SERIE o con el adaptador ST-LINK este último es un programador específico para los microcontroladores de la familia STM32 y STM8 el cual permite realizar procesos de depuración a través de un puerto SWD.

   <figure class="figure col-md-6">
    <img class="img-responsive rounded img-fluid" src="{{site.baseurl}}/images/STM32/st-link-v2.png">
    <figcaption class="figure-caption text-center">Adaptador ST-LINK.</figcaption>
  </figure>
  <figure class="figure col-md-6">
    <img class="img-responsive rounded img-fluid" src="{{site.baseurl}}/images/STM32/conversor-usb-a-serie.png">
    <figcaption class="figure-caption text-center">Conversor USB a serie.</figcaption>
  </figure>

<br>

## Programación de la tarjeta

 Como entorno de desarrollo usaremos Platformio en Visual estudio code, la primera parte consiste en instalar las Herramientas necesarias para manejar las  placas STM32.
   1. Instalar la extensión de Platformio para Visual studio code
      <figure class="figure"> 
      <img class="img-responsive rounded img-fluid" src="{{site.baseurl}}/images/STM32/extensionPlatformio.png">
      <figcaption class="figure-caption text-center">Instalación extensión Platformio</figcaption>
      </figure>

   2. Instalar herramientas de desarrollo para las placas STM32
         <figure class="figure"> 
      <img class="img-responsive rounded img-fluid" src="{{site.baseurl}}/images/STM32/platformio_plataform.png">
      <figcaption class="figure-caption text-center">Instalación plataforma STM32</figcaption>
      </figure>
   3. Crear un nuevo proyecto, seleccionando en board: **STM32F103C8 (20k RAM. 64k Flash) (Generic)** y FlameWork: **Arduino**.
      <figure class="figure"> 
      <img class="img-responsive rounded img-fluid" src="{{site.baseurl}}/images/STM32/nuevoProyecto.png">
      <figcaption class="figure-caption text-center">Configuración nuevo proyecto</figcaption>
      </figure>
   4. En el archivo **platformio.ini** .
   
          upload_protocol = stlink

          debug_tool = stlink
      <figure class="figure"> 
      <img class="img-responsive rounded img-fluid" src="{{site.baseurl}}/images/STM32/platformio_ini.png">
      <figcaption class="figure-caption text-center">platformio.ini</figcaption>
      </figure>
    
 La tarjeta desarrollo cuenta con un led conectado al pin PC13, en la siguiente imagen se puede observar el diagrama de entradas y salidas de la tarjeta.
 <figure class="figure">
    <img class="img-responsive rounded img-fluid" src="{{site.baseurl}}/images/STM32/STM32F103C8T6_PINOUT.png">
    <figcaption class="figure-caption text-center">Pinout tarjeta de desarrollo</figcaption>
  </figure>

### Código:
{% highlight CPP %}
#include <Arduino.h>
void setup()
{
  pinMode(PC13, OUTPUT);
}
void loop()
{
  digitalWrite(PC13, HIGH);
  delay(1000);
  digitalWrite(PC13, LOW);
  delay(1000);
}
{% endhighlight %}

### Subiendo el código

Conectamos la tarjeta con el programador ST-LINK V2, y con el botón de upload de platformio subimos el programa a la tarjeta.
 <figure class="figure">
    <img class="img-responsive rounded img-fluid" src="{{site.baseurl}}/images/STM32/load.png">
    <figcaption class="figure-caption text-center">Programación STM32F101C8T6</figcaption>
  </figure>


<h3>Referencias</h3>
<ul>
  <li> <a href="https://platformio.org/" target="_blank">Platformio</a></li>
  <li> <a href="https://docs.platformio.org/en/latest/boards/ststm32/genericSTM32F103C8.html" target="_blank"> Platformio STM32</a></li>

  <li> <a href="https://www.st.com/resource/en/datasheet/stm32f103c8.pdf" target="_blank"><i class="fa fa-download" aria-hidden="true"></i> Hoja de datos</a></li>
  <li> <a href="https://www.st.com/content/ccc/resource/technical/document/reference_manual/59/b9/ba/7f/11/af/43/d5/CD00171190.pdf/files/CD00171190.pdf/jcr:content/translations/en.CD00171190.pdf" target="_blank"><i class="fa fa-download" aria-hidden="true"></i> Manual de referencia</a></li>
    <li> <a href="http://reblag.dk/wordpress/wp-content/uploads/2016/07/The-Generic-STM32F103-Pinout-Diagram.pdf" target="_blank"><i class="fa fa-download" aria-hidden="true"></i> PINOUT PDF (http://reblag.dk/stm32/)</a></li>

</ul>
<h3>Código</h3>
<ul>
  <li><a href="https://github.com/unelectronica/notas-microcontroladores/tree/master/STM32F108C8/blinkLed" target="_blank"><i class="fa fa-github" aria-hidden="true"></i> Blink STM32</a></li>
</ul>


