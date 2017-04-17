---
layout: post
title: Instalación Energia
img: Energia.png
categories: TivaC ToolChain Energia
tags: TivaC ToolChain Energia
---
<h2>Instalación herramientas de desarrollo TivaC LaunchPad</h2>
Aunque generalmente prefiero trabajar directamente con el codigo C y los ToolChain GCC, en esta página trabajare con un entorno de desarrollo basado en el Ide de Arduino llamado  [Energia](http://energia.nu/)
* Descargamos e instalamos el Ide siguiendo las instrucciones según el sistema operativo. [Descargar Energia](http://energia.nu/download/)  
* Seleccionamos la tarjeta con la que vamos a trabajar ya sea la TM4C123 o la TM4C129.

 <img src="{{site.baseurl}}/images/SeleccionarPlacaEnergia" width="800" align="center">
* Para los usuarios en linux de 64 bits  se nos puede presentar el siguiente error :
`arm-none-eabi-g++: No such file or directory`

Lo solucionamos desde la consola  

{% highlight sh %}
sudo dpkg --add-architecture i386   
sudo apt-get update  
sudo apt-get install libc6:i386

{% endhighlight %}
