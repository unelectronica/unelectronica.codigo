---
layout: post
title: LED RGB TM4C123 LAUNCH PAD
img: TivaRGB.png
categories: TivaC
tags: TivaC
---


La tarjeta TM4C123 cuenta con un led RGB, en el IDE Energía tenemos configurados los 3 pines del led RGB
como `RED_LED` , `GREEN_LED`, `BLUE_LED`, con la combinación de estos 3 bit podemos obtener 8 colores.

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
Watch my video on instlallation
<iframe width="100%" height="360" src="https://www.youtube.com/embed/cweOei34z1E" frameborder="0" allowfullscreen></iframe>
