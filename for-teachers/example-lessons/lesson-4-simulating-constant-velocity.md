# Lesson 4: Simulating Constant Velocity

In this lesson, students will put together what they have learned in the previous lessons and begin simulating motion.

* Students will learn how to give a Particle object a velocity.
* Students will learn how to update the position of a particle based on its velocity.
* Students will learn how to use the function `drawArrow()` to represent velocity vectors.

In the previous tutorial, you learned that you can get Tychos to do repetitive calculations, updating the values of variables with new values based on the calculations that were performed. In this lesson, you are going to see that you can get Tychos to perform a repetitive calculation to update the position of a particle, and thus simulate motion. 

## Velocity is a Rate of Change

Let's return to the definition of velocity, which we can use to calculate the change in distance that a particle will experience in a given change in time. Below is the mathematical representation of a particle's velocity in the x dimension:

![LaTeX: v\_x=\frac{\Delta x}{\Delta t}](https://srcs.instructure.com/equation_images/v_x%253D%255Cfrac%257B%255CDelta%2520x%257D%257B%255CDelta%2520t%257D)

We can calculate how far the particle will travel during a specific change in time by simply representing the change in position as:

![LaTeX: \Delta x\:=\:v\_x\cdot\Delta t](https://srcs.instructure.com/equation_images/%255CDelta%2520x%255C%253A%253D%255C%253Av_x%255Ccdot%255CDelta%2520t)

The larger the velocity in the x direction, then the larger the position change for the given interval of time.

We are now going to also state that what is true in the x dimension is true for the y dimension \(and the z dimension\) as well because space is uniform and we can say that our x or y or z dimensions are really quite arbitrary:

![LaTeX: \Delta y\:=\:v\_y\cdot\Delta t](https://srcs.instructure.com/equation_images/%255CDelta%2520y%255C%253A%253D%255C%253Av_y%255Ccdot%255CDelta%2520t)

\(and ![LaTeX: \Delta z\:=\:v\_z\cdot\Delta t](https://srcs.instructure.com/equation_images/%255CDelta%2520z%255C%253A%253D%255C%253Av_z%255Ccdot%255CDelta%2520t)\)

Because we are working in a 2D space, let's represent our change in 2D space by the matrix ![LaTeX: \vec{\Delta s}](https://srcs.instructure.com/equation_images/%255Cvec%257B%255CDelta%2520s%257D):

![LaTeX: \vec{\Delta s}\:=\:\left\[\Delta x,\:\Delta y\right\]](https://srcs.instructure.com/equation_images/%255Cvec%257B%255CDelta%2520s%257D%255C%253A%253D%255C%253A%255Cleft%255B%255CDelta%2520x%252C%255C%253A%255CDelta%2520y%255Cright%255D)

If our particle's position is given as the vector ![LaTeX: \vec{s}](https://srcs.instructure.com/equation_images/%255Cvec%257Bs%257D), then we can calculate the new position of the particle by simply adding the change in position given by  ![LaTeX: \vec{\Delta s}](https://srcs.instructure.com/equation_images/%255Cvec%257B%255CDelta%2520s%257D):

![LaTeX: \vec{s\_f}=\vec{s\_i}+\vec{\Delta s}](https://srcs.instructure.com/equation_images/%255Cvec%257Bs_f%257D%253D%255Cvec%257Bs_i%257D%252B%255Cvec%257B%255CDelta%2520s%257D)

Let's say that a particle's initial position is \[0, 0\] and it's position is changing at the rate of 10 meters per second in the x direction and 5 meters per second in the y direction. We want to track the movement of the particle by identifying the position at 0.1 second intervals. The table below shows the particle's position from 0 to 1 second:

| Time | x position | y position |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0.1 s | ![](https://srcs.instructure.com/equation_images/0m%255C%253A%252B%255C%253A%255Cleft%28.1s%255C%253A%255Ccdot%255Cfrac%257B%255C%253A10m%257D%257Bs%257D%255Cright%29%253D1m) | ![](https://srcs.instructure.com/equation_images/0m%255C%253A%252B%255Cleft%28.1s%255C%253A%255Ccdot%255Cfrac%257B%255C%253A5m%257D%257Bs%257D%255Cright%29%253D.5m) |
| 0.2 s | ![](https://srcs.instructure.com/equation_images/1m%255C%253A%252B%255C%253A%255Cleft%28.1s%255C%253A%255Ccdot%255Cfrac%257B%255C%253A10m%257D%257Bs%257D%255Cright%29%253D2m) | ![](https://srcs.instructure.com/equation_images/.5m%255C%253A%252B%255Cleft%28.1s%255C%253A%255Ccdot%255Cfrac%257B%255C%253A5m%257D%257Bs%257D%255Cright%29%253D1m) |
| 0.3 s | ![](https://srcs.instructure.com/equation_images/2m%255C%253A%252B%255C%253A%255Cleft%28.1s%255C%253A%255Ccdot%255Cfrac%257B%255C%253A10m%257D%257Bs%257D%255Cright%29%253D3m) | ![](https://srcs.instructure.com/equation_images/1m%255C%253A%252B%255Cleft%28.1s%255C%253A%255Ccdot%255Cfrac%257B%255C%253A5m%257D%257Bs%257D%255Cright%29%253D1.5m) |
| 0.4 s | ![](https://srcs.instructure.com/equation_images/3m%255C%253A%252B%255C%253A%255Cleft%28.1s%255C%253A%255Ccdot%255Cfrac%257B%255C%253A10m%257D%257Bs%257D%255Cright%29%253D4m) | ![](https://srcs.instructure.com/equation_images/1.5m%255C%253A%252B%255Cleft%28.1s%255C%253A%255Ccdot%255Cfrac%257B%255C%253A5m%257D%257Bs%257D%255Cright%29%253D2m) |
| 0.5 s | ![](https://srcs.instructure.com/equation_images/4m%255C%253A%252B%255C%253A%255Cleft%28.1s%255C%253A%255Ccdot%255Cfrac%257B%255C%253A10m%257D%257Bs%257D%255Cright%29%253D5m) | ![](https://srcs.instructure.com/equation_images/2m%255C%253A%252B%255Cleft%28.1s%255C%253A%255Ccdot%255Cfrac%257B%255C%253A5m%257D%257Bs%257D%255Cright%29%253D2.5m) |
| 0.6 s | ![](https://srcs.instructure.com/equation_images/5m%255C%253A%252B%255C%253A%255Cleft%28.1s%255C%253A%255Ccdot%255Cfrac%257B%255C%253A10m%257D%257Bs%257D%255Cright%29%253D6m) | ![](https://srcs.instructure.com/equation_images/2.5m%255C%253A%252B%255Cleft%28.1s%255C%253A%255Ccdot%255Cfrac%257B%255C%253A5m%257D%257Bs%257D%255Cright%29%253D3m) |
| 0.7 s | ![](https://srcs.instructure.com/equation_images/6m%255C%253A%252B%255C%253A%255Cleft%28.1s%255C%253A%255Ccdot%255Cfrac%257B%255C%253A10m%257D%257Bs%257D%255Cright%29%253D7m) | ![](https://srcs.instructure.com/equation_images/3m%255C%253A%252B%255Cleft%28.1s%255C%253A%255Ccdot%255Cfrac%257B%255C%253A5m%257D%257Bs%257D%255Cright%29%253D3.5m) |
| 0.8 s | ![](https://srcs.instructure.com/equation_images/7m%255C%253A%252B%255C%253A%255Cleft%28.1s%255C%253A%255Ccdot%255Cfrac%257B%255C%253A10m%257D%257Bs%257D%255Cright%29%253D8m) | ![](https://srcs.instructure.com/equation_images/3.5m%255C%253A%252B%255Cleft%28.1s%255C%253A%255Ccdot%255Cfrac%257B%255C%253A5m%257D%257Bs%257D%255Cright%29%253D4m) |
| 0.9 s | ![](https://srcs.instructure.com/equation_images/8m%255C%253A%252B%255C%253A%255Cleft%28.1s%255C%253A%255Ccdot%255Cfrac%257B%255C%253A10m%257D%257Bs%257D%255Cright%29%253D9m) | ![](https://srcs.instructure.com/equation_images/4m%255C%253A%252B%255Cleft%28.1s%255C%253A%255Ccdot%255Cfrac%257B%255C%253A5m%257D%257Bs%257D%255Cright%29%253D4.5m) |
| 1.0 s | ![](https://srcs.instructure.com/equation_images/9m%255C%253A%252B%255C%253A%255Cleft%28.1s%255C%253A%255Ccdot%255Cfrac%257B%255C%253A10m%257D%257Bs%257D%255Cright%29%253D10m) | ![](https://srcs.instructure.com/equation_images/4.5m%255C%253A%252B%255Cleft%28.1s%255C%253A%255Ccdot%255Cfrac%257B%255C%253A5m%257D%257Bs%257D%255Cright%29%253D5m) |

We are calculating the position _iteratively_. As time progresses, we can simply update the postion of the particle for each interval of time that has elapsed - what is called an _iteration_. An iteration is a small _interval_ or a _step_ in the process. The iteration _interval_ is the amount of time represented by ![LaTeX: \Delta t](https://srcs.instructure.com/equation_images/%255CDelta%2520t).

## Iteratively Updating A Particle's Position in Tychos

Doing these calculations over and over again can seem a bit tedious, and as the interval time shortens, then the number of calculations required grows...

But as you have learned in the previous tutorial, computers are really good at doing these kinds of repetitive calculations. In fact, you can just set up the formula and then have the computer do all the calculations for you.

Click on the link below to open the Tychos scenario in a new broswer tab where you can follow along, or use the embedded frame that contains the scneario below:

[Simulating 2D Constant Velocity](https://tychos.org/scenarios/339)

The first thing that we need to do is create a particle. Let's call the particle `p1`. Type this code in the **Initial State** pane:

```text
p1 = Particle([50, 50], 5, "green")
```

When you press the **Start** button in Tychos, you should see a green particle appear on the world grid. Now we want the particle to move, but we have to define the rate at which it is going to move.

Let's say that we wanted to simulate a particle moving along the x axis with a velocity of 10 meters per second:

![v\:=\frac{\Delta x}{\Delta t}=\frac{\:10m}{1s}](https://canvas.instructure.com/equation_images/v%255C%253A%253D%255Cfrac%257B%255CDelta%2520x%257D%257B%255CDelta%2520t%257D%253D%255Cfrac%257B%255C%253A10m%257D%257B1s%257D)

We can define this velocity as a matrix in code:

```text
v = [10,0]
```

Now we could use this matrix to conduct some calculations on how to update the position of the particle. We are going to introduce here a method commonly used in many programming languages to associate this velocity to the particle _p1_. This way we can see that this velocity "belongs" to the particle `p1` by giving the particle an _attribute_. Change the above line of code so that it now looks like this:

```text
p1.v = [10, 0]
```

The velocity matric `[10, 0]` is now an attribute of the particle, just as the position of the particle is also an attribute that we can access like this:

```text
p1.pos = [0, -50]
```

If you press the **Start** button, you will see that the particle does not move yet. This is because Tychos has no idea what velocity is. You have to define how the velocity is going to update the position. This is done in the **Calculations** pane.

Remember that the simulated world's time is segmented into units called frames. If the frame rate is 20 frames per second, then the change in time \(or `dt`\) is .05 seconds. So if a particle has a velocity of say 10 meters per second, then we need to define how far it would go in .05 seconds. This will be the rate of position change _per frame._

The change in position is the change in the particle's position for that frame, but the velocity is defined as the rate of change _per second_. Add this line of code to the **Calculations** pane:

```text
ds = p1.v*dt
```

In the above code, we are saying that the change in position \(`ds`\) will be calculated by multiplying the particle's velocity by the interval time \(`dt`\). This will calculate the change in position for this _frame_. It is an identical calculation to the one we defined above, but now just in code:

![LaTeX: \left\[\Delta x,\:\Delta y\right\]\:=\left\[v\_x\cdot\Delta t,\:v\_y\cdot\Delta t\right\]](https://srcs.instructure.com/equation_images/%255Cleft%255B%255CDelta%2520x%252C%255C%253A%255CDelta%2520y%255Cright%255D%255C%253A%253D%255Cleft%255Bv_x%255Ccdot%255CDelta%2520t%252C%255C%253Av_y%255Ccdot%255CDelta%2520t%255Cright%255D)

We can now use this to change the current position of the particle by _recalculating_ the position of the Particle every frame. Place this line of code just below the previous line of code, once again in the **Calculations Pane**:

```text
p1.pos = p1.pos + ds
```

When you press the **Start** button you should see the Particle move!

Let's see if this makes sense. Because the frame rate is 1/20 of a second, which is .05 seconds, and the velocity is \[10, 0\], then for a single frame, the particle will move 0.5 units \(10 x .05 = 0.5\) in the x direction. After 2 frames, which is 1/10 of a second, the particle will have moved 1 unit. After 10 frames, which is 1/2 of a second, the particle will have moved 5 units in the x direction. Finally, you should see that after 20 frames, which is 1 second, the particle will have moved 10 units in the x direction. This is precisely what we want. We want the particle to move at 10 units _per second along the x direction_.

Go back to the **Initial State** pane and change the particle's velocity:

```text
p1.v = [10, 5]
```

When you press the **Start** button, you should see the that the particle is now traveling in a diagonal path - it is now traveling in both the x and y dimensions!

Finally, let's add a vector arrow to represent the position vector of the particle. Add this line of code in the **Calculations Pane**just below the last line of code:

```text
drawArrow([0, 0], p1.pos)
```

You will see an arrow that is changing in length that stretches from the origin to the particle's position.

Cool! Now its time to work on some goals to see if you actually get it:

* **Create a particle called p2 with an initial position of \[100, 50\]**
* **Make the particle p2 move so that it returns to the origin after 5 seconds.**
* **Create a particle called p3 with an initial position of \[-70, -100\]**
* **Make the particle p3 move so that its position is \[30, 30\] afte 5 seconds.**

You have successfully simulated particles moving through 2D space at a constant velocity!

### Using Vector Arrows To Represent Velocity

As you learned earlier, Tychos gives us a tool for visualizing a vector quantity. A vector arrow is simply an arrow that points in the direction from a specified origin with the dimensions indicated by the vector quantity - in our case the velocity matrix. We have seen how to draw position vectors that are attached to the origin because this is the point in space where all particle's positions are measured. Velocity however, is _attached_ to the individual particle. It is an attribute of each particle so it would be nice to represent the velocity of each particle by an arrow that is _attached_ to the particle. This can be done like this:

```text
drawArrow(p1.pos, p1.v, "purple")
```

This command draws a vector arrow from the position of the particle and defines the length and direction of the arrow based on the velocity \(represented by the variable "v" here\) and then also gives it a color - in this case "purple".

These vector arrows are used to help represent the motion of the particle, and I think you will find them very useful as we progress through this unit.

Try adding a vector arrow to your moving particles.

### Conclusion

You should now be familiar with the following:

* How to repetitively perform a calculation to update a variable's value each frame.
* Understand that the variable `dt` represents the time interval duration for each frame.
* Understand that the time in seconds in the simulated universe \(virtual time\) is the result of the frame rate multiplied by the time interval \(`dt`\)
* How to change a particle's position by:
  * Defining a velocity matrix for the particle.
  * Multiplying the velocity matrix by the time interval to get the change in position.
  * Add the change in position to the particle's current position in order to update it.
* How to attach velocity vectors to a particle in order to visualize the particle's velocity.

