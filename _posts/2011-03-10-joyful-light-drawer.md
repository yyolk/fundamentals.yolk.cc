---
layout: post
title: Joyful Light Drawer
---

<img src="http://media.tumblr.com/tumblr_lht1pduLTD1qz4ztm.png" />
<div class='player'><iframe src="http://player.vimeo.com/video/20846305?portrait=0&amp;color=ffffff&amp;loop=1" width="500" height="500" frameborder="0"></iframe></div>

{% highlight java %}
//Joyful Light Drawer
//Derived from "Experiment in Abstract Shading" code.
//A lissajous curve modified to respond to mouseX, mouseY

float t = 0.2;
float spX, spY;

float stopVal;

int myFill;
//color lookup array
color[] colors = new color[5];


//how many circles to use when drawing
int count = 100;

void setup(){
  frameRate(15);
  size(500,500);
  smooth();
  stopValSet();
  myFill = 0;
  //the colors to be used
  colors[0] = #DAF799;
  colors[1] = #5FFAC6;
  colors[2] = #394541;
  colors[3] = #C45923;
  colors[4] = #F55302;
  
  background(255);
}

void draw(){
     // change the background color every 100 frames
     if(frameCount%100==0){
       switchColor();
     }
       fill(myFill,10);

       strokeWeight(20);
       rect(0,0,width,height);
       
       strokeWeight(5);
    
    //create a lissajous curve

    for (int i = 0; i< count; i++){ 
     

    
     spX = (t* mouseX*width) * 0.000001;
     spY = (t* mouseY*width) * 0.000001;
     spX = (width/2)*sin(spX);
     spY = (height/2)*cos(spY);



     stroke(colors[floor(random(colors.length))]);

     strokeWeight(5);

     point(spX + width/2 , spY + height/2);
     t += .1;

    }

    //reset theta if it is greater than stopVal
    if(t > stopVal){
      t = 0.1;

    }  

    

}

void switchColor(){
  if (myFill == 0){
    myFill = 255;
  } else {
    myFill = 0;
  }
}

void stopValSet(){
  stopVal = 50000;
}
{% endhighlight %}