---
layout: post
title: An Experiment in Abstract Shading
---

<p><img src="http://media.tumblr.com/tumblr_lgrquqrSCJ1qz4ztm.png" />
<div class='player'><iframe src="http://player.vimeo.com/video/20823299?portrait=0&amp;color=ffffff&amp;loop=1" width="500" height="500" frameborder="0"></iframe></div>
</p>&#13;

{% highlight java %}
//A experiment in abstract shading.

float t = 0.2;
float spX, spY;

float stopVal;

//color lookup array
color[] colors = new color[5];


//how many circles to use when drawing
int count = 100;

void setup(){
  
  size(500,500);
  smooth();
  stopValSet();

  //the colors to be used
  colors[0] = #811421;
  colors[1] = #a81e2e;
  colors[2] = #aedfe4;
  colors[3] = #58b6dd;
  colors[4] = #00b0d8;
  
  background(255);
}

void draw(){
  
     //draw consecutive lines, horizontally - and only on the first frame
     if(frameCount==1){
     
       strokeWeight(5);
     
       for(int i = 0; i<60; i+=1){
         //draw the line with x values 0 and the width of the sketch
         //y1, y2 is determines by i
         line(0,(i*10),width,(i*10));
       }
     
     }
    
    //create a lissajous curve
    for (int i = 0; i< count; i+=1){ 
     

     spX = (t* cos(spX)) * 0.001;
     spY = (t* sin(spX)) * 0.001;

     spX = height/2 * sin(spX);
     spY = width/2 * cos(spY);

     //fill for the circles - black with 40% opacity
     fill(0,40);
     stroke(colors[floor(random(colors.length))],45);

     strokeWeight(5);
     ellipse(spX+width/2,spY+height/2, 20,20);
     point(spX + width/2, spY+height/2);
     t += 0.3;
     println(t);  
    }

    //reset theta if it is greater than stopVal
    if(t > stopVal){
      t = 0.2;
      stopValSet();
    }  
    
    

}

void stopValSet(){
  stopVal = random(2000,5500);
  //stopVal = 5000;
}
{% endhighlight %}