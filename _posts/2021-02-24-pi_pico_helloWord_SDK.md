---
layout: post
title: HOLA MUNDO RASPBERRY PI PICO
img: pi_pico/sdk_pi_pico.png
categories: PI_PICO
tags: Pico
---  

La raspberry pi pico es una tarjeta de desarrollo de la fundación Raspberry pi basada en el RP2040, el cual es un microcontrolador dual core diseñado por la fundación.

### Características principales del  RP4020

+ Dual core ARM Cortex M0
+ Reloj flexible de 133 MHz
+ 264KB de SRAM
+ 2MB de memoria flash
+ USB 1.1
+ 26 GPIOs
+ 2 SPI
+ 2 I2C
+ 3 ADC de 12 bits
+ 16 canales PWM
  
 <figure class="figure">
   <img class="websocket pruebas" src="{{site.baseurl}}/images/pi_pico/Pi-Pico-pinout-diagram.png">
</figure>


## Herramientas de desarrollo

Actualmente la tarjeta se puede programar usando Micropython y un SDK de C, aunque se a anunciado que próximamente se integrará al IDE de Arduino.



### Instalación SDK C

se procede a instalar en Ubuntu 20.04 las herramientas necesarias para el trabajo con la SDK **pico_sdk** 

+ Compilador gcc para procesadores arm
+ CMake
+ build-essential

``` sh
sudo apt install cmake gcc-arm-none-eabi libnewlib-arm-none-eabi build-essential
```

Clonamos el repositorio del SDK pico-sdk

```sh
git clone -b master https://github.com/raspberrypi/pico-sdk.git
cd pico-sdk
git submodule update --init

```
Se añade  la siguiente linea al archivo **.bashrc**

```
export PICO_SDK_PATH={ruta sdk}/pico-sdk
```

### Instalación extensiones de VisualStudio Code

Para trabajar con la tarjeta  usaremos el Ide de  VisualStudio Code, se instalan las siguientes extensiones que nos facilitan el trabajo con cmake

``` sh
  code --install-extension marus25.cortex-debug
  code --install-extension ms-vscode.cmake-tools
  code --install-extension ms-vscode.cpptools
```

### Hola mundo
En este ejemplo se hace parpadear el led que viene con la tarjeta, el cual se encuentra conectado al pin 25 del microcontrolador.
Se crea una carpeta y se abre con VisualStudio code, se crean los siguientes archivos :

**CMakeLists.txt**

{% highlight CMake %}
cmake_minimum_required(VERSION 3.1)

include({path pico_sdk}/external/pico_sdk_import.cmake)

project(blink)

pico_sdk_init()

add_executable(main
    main.c
)


pico_add_extra_outputs(main)
target_link_libraries(main pico_stdlib)

{% endhighlight %}

**main.c**

{% highlight CPP %}
#include "pico/stdlib.h"
#include "hardware/gpio.h"

int main() {
    const uint LED_PIN = 25;
    gpio_init(LED_PIN);
    gpio_set_dir(LED_PIN, GPIO_OUT);

    while (true) {
        gpio_put(LED_PIN, 1);
        sleep_ms(100);
        gpio_put(LED_PIN, 0);
        sleep_ms(100);
    }
    return 0;
}
{% endhighlight %}

 luego de creado los dos archivos se procede a hacer click  en el botón **versión de compilación**
 <figure class="figure">
   <img class="websocket pruebas" src="{{site.baseurl}}/images/pi_pico/build_vcode.png">
</figure>

Por ultimo se conecta la tarjeta al puerto usb manteniendo pulsado el botón blanco, el computador la reconocerá como un medio de almacenamiento y se procede a copiar el archivo **main.uf2** que se genero la carpeta **build** del proyecto.

<iframe width="560" height="315" src="https://www.youtube.com/embed/S-q6hmXemwY" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
  
<h3>Referencias</h3>
  
  <a href="https://datasheets.raspberrypi.org/pico/getting-started-with-pico.pdf" target="_blank"><i class="fa fa-file" aria-hidden="true"></i> https://datasheets.raspberrypi.org/pico/getting-started-with-pico.pdf</a>

  <a href="https://datasheets.raspberrypi.org/pico/pico-datasheet.pdf" target="_blank"><i class="fa fa-file" aria-hidden="true"></i> https://datasheets.raspberrypi.org/pico/pico-datasheet.pdf</a>
  

  <a href="https://www.raspberrypi.org/products/raspberry-pi-pico/" target="_blank"><i class="fa fa-link" aria-hidden="true"></i> https://www.raspberrypi.org/products/raspberry-pi-pico</a>

<a href="https://github.com/raspberrypi/pico-sdk" target="_blank"><i class="fa fa-github" aria-hidden="true"></i> https://github.com/raspberrypi/pico-sdk</a>

  <a href="https://github.com/raspberrypi/pico-examples" target="_blank"><i class="fa fa-github" aria-hidden="true"></i> https://github.com/raspberrypi/pico-examples</a>

  <a href="https://github.com/unelectronica/notas-microcontroladores/tree/master/PI_PICO/blink" target="_blank"><i class="fa fa-github" aria-hidden="true"></i> código blink</a>