---
layout: post
title: LED RGB TM4C123 LAUNCH PAD
img: TivaRGBv2.png
categories: TivaC
tags: TivaC
---


La tarjeta TM4C123 cuenta con un led RGB, en el IDE Energía tenemos configurados los 3 pines del led RGB
como <mark>RED_LED</mark>, <mark>GREEN_LED</mark>, <mark>BLUE_LED</mark> , con la combinación de estos 3 bit podemos obtener 8 colores.

<figure class="figure">
<img class="img-responsive img-rounded" src="{{site.baseurl}}/images/scheaticRGBTM4C123.png">
<figcaption class="figure-caption text-center">Esquemático led RGB TM4C123</figcaption>
</figure>
<br>

{% highlight CPP %}

/*Hola mundo TivaC RGB*/
#define MASK_R 0X01
#define MASK_G 0X02
#define MASK_B 0X04

void setup() {
 pinMode(RED_LED,OUTPUT);
 pinMode(GREEN_LED,OUTPUT);
 pinMode(BLUE_LED,OUTPUT);
}

void loop() {
  unsigned i;
  for(i=0;i<8;i++){
    writeRGB(i);
    delay(500);
  }

}
void writeRGB(unsigned int num){
  digitalWrite(RED_LED, num & MASK_R);
  digitalWrite(GREEN_LED, num & MASK_G);
  digitalWrite(BLUE_LED, num & MASK_B);
}
 {% endhighlight %}


[GitHub code: Hola Mundo RGB](https://github.com/unelectronica/notas-microcontroladores/tree/master/TM4C123GXL%20/HolaMundoRGB)

<iframe width="100%" height="360" src="https://www.youtube.com/embed/cweOei34z1E" frameborder="0" allowfullscreen></iframe>
