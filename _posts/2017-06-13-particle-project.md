---
layout: post
title: Designing Particle Simulation in Processing
excerpt: "A fun project to help develop fluency in data structures and algorithms"
categories: [Processing]
comments: true
 image:
  feature: http://i.imgur.com/Sjb82wv.png
  <!--  credit: Powder Toy
  creditlink: http://powdertoy.co.uk/ -->
---
 
Lately I've been working on a [Processing](https://processing.org/) project for an Introduction to Programming course. Basically, the idea is to create a simple system for particles to interact with each other, inspired by that game everyone played in high school at one point, the [Powder Toy](powdertoy.co.uk). Of course, having just started my degree this year, I wouldn't be able to simulate things like fluid dynamics! So instead, I decided to set the bar a bit lower, and just use this project to become more familiar with data structures. 

Now, understandably, having just learned about how data can be stored in these wonderful data structures called arrays, I was completely ready to begin programming particle physics. For most in-class assignments, we had been mainly using arrays to store all our information. For example, in one of our exercisees, we were to make many floating bubbles appear on the screen at once, like so:

<iframe src="https://www.openprocessing.org/sketch/426978/embed/" width="100%" height="400"></iframe>

I stored the position of each bubble in an array, and use a for-loop to iterate through every array and update data such as the position of each bubble on the screen and its size. Although, I figured I'm going to need a lot more than just arrays to make my particle simulation. My general idea was to create a 'Particle' class which contained information such as it's position, speed, acceleration, colour size and other useful information a particle would want. The problem was where to store all these particles. Originally, I decided to use an ArrayList, looping through every entry and updating their data. Most of the pseudocode looked a little like this:

    if <particle> is within 20 pixels of another particle {
      Use trigonometry to bounce the particle off in the opposite direction
    } else {
      Accelerate down the screen
    }
    
There was a whole lot of 'if' statements, for loops and commented code everywhere - the end result was very laggy and didn't really have much potential. At all. I turned to my practical demonstrators for a bit of help - one of them enthusiastically suggested that I should look into using hashmaps. Instead of intensively simulating circles on the screen and relying on Euclidean distance, characteristics of particles could instead be stored within a hashmap. For example, their x- and y-position. The only problem was my approach. My first attempt basically relied on calculating collisions based on whether two particles were in the same square, like so:

<a href="http://imgur.com/emx6jXe"><img src="http://i.imgur.com/emx6jXe.png" title="source: imgur.com" width="300px"/></a>

I realised that a better way of checking for collisions was to do it before the particles moved into another square:

    if (square directly below particle is empty) {
      Move down
    } else {
      Move to the right or left but do not move down
    }

This method resulted in something that was actually starting to look good! There were just a few problems which I didn't end up fixing before handing in this assignment:

* Particles sometimes disappeared as time went on. The problem was that two particles could occasionally move into the same square at *just* the right time, causing one particle to be 'swallowed' up by the other. I never really solved this problem in the end, but instead used a bandaid solution: if this occured, then create a new particle on top of the overlapped particle. This resulted in some rather odd jumpy situations during the simnulation. 
* Particle size could not be made smaller than a certain amount of pixels, as this would then amplify the above problem.
* Speed was defined using the traditional distance per time, except with distance being represented by pixels. Perhaps a better solution would be to define speed using actual milliseconds instead. 
* Sometimes it takes a while for the water to spread out into a line.

There are a whole lot of other issues of course, most of them stemming how I designed my algorithms. There's also probably a lot of novice mistakes here and there, but as my first 'big' programming project that I've worked on, I'm pretty happy with the final result. Here is the live version - left click for water particles, right click for stationary particles:

<iframe src="https://www.openprocessing.org/sketch/432537/embed/" width="550" height="550"></iframe>

My presentation slides can be found [here](bit.ly/particlepres). Maybe one day when I'm a much better programmer, I'll come back to this project!
