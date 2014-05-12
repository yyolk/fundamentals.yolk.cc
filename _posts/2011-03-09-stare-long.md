---
layout: post
title: Stare Long
---

<img src="http://media.tumblr.com/tumblr_lhs31ouIzP1qz4ztm.png" />
<div class='player'><iframe src="http://player.vimeo.com/video/20823352?portrait=0&amp;color=ffffff&amp;loop=1" width="500" height="500" frameborder="0"></iframe></div>

{% highlight java %}
// Sketch2
// CONTROLS:
// Click on the canvas to pause/unpause
// r = saves the current frame
// any other key while paused = step forward one frame

// This runs through draw to create a canvas filled with little shape. 
// I swear I see things if I stare at this long enough.


float shapeSize;
PShape oblong;
boolean pause;

void setup()

{
  size(500, 500);

  background(0);  
  frameRate(15);
  oblong = loadShape("wave.svg");
  oblong.disableStyle();


  noStroke();
  smooth();

}

void draw()
{
  // cycle through the vertical
  for (float x = 0; x < height; x+=shapeSize){
    // then the horizontal
    for ( float y = 0; y < width; y+=shapeSize ){
      
      // set the size of the shape
      shapeSize = random(1,25);
      
      // randomly select the color to fill the shape
      switch(floor(random(3))){
      case 0:
        fill(random(255),random(255),random(255));
        break;
      case 1:
        fill(0);
        break;
      case 2:
        fill(255);
        break;
      }

      // draw the shape
      shape(oblong, x, y, shapeSize, shapeSize);

    }
  }

}

void keyPressed(){
  if(key=='r'){
    saveFrame();
  }
  else{
    redraw();
  }
}


void mouseClicked(){
  if(pause){
    loop();
  } 
  else {
    noLoop();
  }
  pause = !pause;
}
{% endhighlight %}