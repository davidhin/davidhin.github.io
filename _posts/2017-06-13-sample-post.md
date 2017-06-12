---
layout: post
title: Designing Particle Simulation in Processing Part 1
excerpt: "A fun project to help develop fluency in data structures and algorithms"
categories: [Processing]
comments: true
image:
  feature: http://i.imgur.com/HsoPreD.png
  credit: Powder Toy
  creditlink: http://powdertoy.co.uk/
---
 
Lately I've been working on a [Processing](https://processing.org/) project for an Introduction to Programming course. Basically, the idea is to create a simple system for particles to interact with each other, inspired by that game everyone played in high school at one point, the [Powder Toy](powdertoy.co.uk). Of course, having just started my degree this year, I wouldn't be able to simulate things like fluid dynamics! So instead, I decided to set the bar a bit lower, and just use this project to become more familiar with data structures. 

Now, understandably, having just learned about how data can be stored in these wonderful data structures called arrays, I was completely ready to begin programming particle physics. For most in-class assignments, we had been mainly using arrays to store all our information. For example, in one of our exercisees, we were to make many floating bubbles appear on the screen at once, like so:

<iframe src="https://www.openprocessing.org/sketch/426978/embed/" width="100%" height="400"></iframe>

I stored the position of each bubble in an array, and use a for-loop to iterate through every array and update data such as the position of each bubble on the screen and its size. 

Although, I figured I'm going to need a lot more than just arrays to make my particle simulation. My general idea was to create a 'Particle' class which contained information such as it's position, speed, acceleration, colour size and other useful information a particle would want. The problem was where to store all these particles. Originally, I decided to use an ArrayList, looping through every entry and updating their data. Most of the pseudocode looked a little like this:

    if <particle> is within 20 pixels of another particle {
      Use trigonometry to bounce the particle off in the opposite direction
    } else {
      Accelerate down the screen
    }
    
There was a whole lot of 'if' statements, for loops and commented code everywhere - the end result was very laggy and didn't really have much potential. At all. 
