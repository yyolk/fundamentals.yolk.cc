---
layout: post
title: Stare Long II
---

<img src="http://media.tumblr.com/tumblr_li709mbzh31qz4ztm.png" />
<div class='player'><iframe src="http://player.vimeo.com/video/21175667?byline=0&amp;portrait=0&amp;color=ffffff&amp;loop=1" width="500" height="500" frameborder="0"></iframe></div>

{% highlight java %}
// Sketch 4 - "Stare Long II"


NP foo[];

float rot;

void setup(){
  size(500,500);
  foo = new NP[12];

  for(int i = 0; i < foo.length; i++){
    foo[i] = new NP(2.2, random(3.3*i*i), random(4.1*i*i), random(1), round(random(80)), round(random(random(100))));
  }

  frameRate(60);

  background(0);
  smooth();
  rot = PI*.90;
}


void draw(){
  if (mousePressed){
    noStroke();
    fill(0,10);
    rect(0,0,width,height);
  } 
  else {
    strokeWeight(10);
    noFill();
    rect(0,0, width, height);
  }
  if( frameCount % 2 == 0){
    fill(0,1);
    rect(0,0,width,height);
  }
  translate(width/2, height/2);

  rotate(rot);
  rot += PI*.8;

  for (int i = 0; i<foo.length; i++){
    rotate(HALF_PI/4);
    foo[i].draw();

  }
  



}


class NP{
  float s1;
  float s2;
  float s3;
  float v1;
  float x, y, a;
  int seed;
  int nseed;
  color[] carray;
  
  NP(float s1, float s2, float s3, float v1, int seed, int nseed){
    this.s1 = s1;
    this.s2 = s2;
    this.s3 = s3;
    
    this.v1 = v1;
    
    this.seed = seed;
    this.nseed = nseed;
    carray = new color[5];

//    carray[0] = color(#556270) ;
//    carray[1] = color(#4ECDC4) ;
//    carray[2] = color(#C7F464) ;
//    carray[3] = color(#FF6B6B) ;
//    carray[4] = color(#C44D58) ;

    carray[0] = color(#ffffff);
    carray[1] = color(#FF5555);
    carray[2] = color(#FFF7F7);
    carray[3] = color(#000000);
    carray[4] = color(#FF5555);
    
  }
  
  void generate(){
    randomSeed(seed);
    noiseSeed(nseed);
    s1 += random(0.001, 0.01)*.1;
    s2 += random(0.01, 0.001)*.2;
    s3 += random(.001, 0.01);
    x = noise(s1) * (width);
    y = noise(s2) * (height);
    a = noise(s3) * (min(width,height));
    v1 = noise(random(1))*255;

  }
  
  void draw(){


    generate();
    noFill();
    stroke(255);
    strokeWeight(constrain(v1, 1, 2.4));



    rotate(PI/2);
    stroke(255, v1);
    y = y % height/2;
    x = x % width/2;
    a = a % min(width, height)/2;
    
    switch(floor(random(4))){
      case 0:
        beginShape(QUAD_STRIP);
        break;
      case 1:
        beginShape(POINTS);
        break;
      case 2:
        beginShape(LINES);
        break;
      case 3:
        beginShape(POINTS);
        break;
    }
    


    stroke(carray[floor(random(5))],v1);
    vertex(x,y);
    vertex(y,x);

    stroke(carray[floor(random(5))],v1);
    vertex(a,x);

    stroke(carray[floor(random(5))],v1);
    vertex(a,y);
    stroke(carray[floor(random(5))],v1);

    vertex(y,a);
    stroke(carray[floor(random(5))],v1);

    vertex(x,a);
    stroke(255,v1);
    endShape();

  }
}
{% endhighlight %}