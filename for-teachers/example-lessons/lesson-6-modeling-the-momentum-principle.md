# Lesson 7: Modeling A Projectile

## Lesson Objectives and Overview

Students finally get to see how a force can be modeled in Tychos and how the change in a particle's state can be calculated using the momentum principle.

* Students will learn how to define a mass attribute for a particle.
* Students will learn how to calculate a change in momentum due to an applied force.
* Students will learn how to update a particle's velocity based on a change in momentum caused by the force.

We have seen that we can simulate a particle's behavior when it is acted upon by forces in two dimensions. When the NET force on the particle points diagonally in space, then we can see that the object's momentum will change in both dimensions.

In the animation below, we see a particle that starts off from rest. Two forces are acting on it - identified by the two black arrows. The NET force acting on the particle is identified by the red arrow. Notice that the green arrow, which represents the velocity of the particle points in the same direction, but its length is increasing.

In the previous lesson we only looked at the special case when the initial momentum of the particle was zero, like in the above example. What happens when the initial momentum \(and therefore the initial velocity\) of the particle is not zero? How does the particle behave if the force points in a direction that is not in the same direction as the object's initial momentum?

Recall from the previous lesson that the Momentum Principle states that a force applied for a specific amount of time will change the momentum of a particle by a specific amount:

![LaTeX: m\cdot\Delta v\:=\:\sum F\:\cdot\Delta t](https://srcs.instructure.com/equation_images/m%255Ccdot%255CDelta%2520v%255C%253A%253D%255C%253A%255Csum%2520F%255C%253A%255Ccdot%255CDelta%2520t)

or in code:

```text
dp = Fnet * dt
```

The momentum principle, as we have stated before is a very powerful principle that helps us understand the cause and effect relationship between forces acting on an object, and how that object's state of motion is changing. You might think that a changing velocity is equivalent to either speeding up or slowing down. A change in momentum though can also mean a change in the _direction_ of the object's momentum. 

In this tutorial we will investigate how to simulate a particle that already has a momentum \(an initial velocity that is NOT zero\) and whose momentum is changing when a net force acts on the particle along a direction that is other than the direction of the object's momentum.

This is precisely the case in projectile motion. We are going to look specifically at how to simulate a projectile's motion.

## Simulating Surface Gravity

To follow along in this tutorial, open the scenario in a new tab by clicking on the link below:

[Tutorial - Simulating A Projectile](https://tychos.org/scenarios/489)

We are going to define a particle that is being acted upon by only gravity. This is one of the defining principles of projectiles.

In order to do this, we are first going to review how we simulate a particle in Tychos. The first thing that you are going to need to do is create a particle that we can apply our force on. For review, see if you can remember how to do this by achieving this goal:

* **Create a particle called "ball" with an initial position of \[0, 0\] a radius of 5 and a 'mass' of 5."**

The next step in the **Initial State** pane is to give the ball a velocity that is \[0, 0\]. We are going to change this soon, but for now, just make it zero like this:

```text
ball.v = [0, 0]
```

To define the gravitational force, we need to use a matrix, but whose value is dependent on the mass of the particle. Hopefully you recall that the force of gravity for an object close to the surface of the earth is given by this simple calculation:

![LaTeX: \vec{F\_{gravity}}=mass\:\cdot\:\left\[0,\:-\frac{9.8\:m}{s^2}\right\]](https://srcs.instructure.com/equation_images/%255Cvec%257BF_%257Bgravity%257D%257D%253Dmass%255C%253A%255Ccdot%255C%253A%255Cleft%255B0%252C%255C%253A-%255Cfrac%257B9.8%255C%253Am%257D%257Bs%255E2%257D%255Cright%255D)

The equation above states that the force of gravity is indeed a vector that points in the negative vertical direction but has no horizontal component. The gravitational force acting on a ball with a mass of 2 kg would then be:

![LaTeX: \vec{F\_{gravity}}=2 kg\:\cdot\:\left\[0,\:-\frac{9.8\:m}{s^2}\right\] =\left\[0, -19.6 N\right\]](https://srcs.instructure.com/equation_images/%255Cvec%257BF_%257Bgravity%257D%257D%253D2%2520kg%255C%253A%255Ccdot%255C%253A%255Cleft%255B0%252C%255C%253A-%255Cfrac%257B9.8%255C%253Am%257D%257Bs%255E2%257D%255Cright%255D%2520%253D%255Cleft%255B0%252C%2520-19.6%2520N%255Cright%255D)

To define this force in code, we just multiply the ball's mass by the vector \[0, -9.8\]:

```text
# Define the force of gravity
Fg = ball.mass * [0, -9.8]
```

If the ball's mass were to change \(let's say we filled it with virtual cement!\), the force of gravity would change accordingly, just as it would in the real world.

In order for the particle to respond to the gravitational force we just need to once again, define the momentum principle in the **Calculations Pane**. We then define a change in momentum in code like this:

```text
# Define a change in momentum due to gravity
dp = Fg * dt
```

The interval time is of course the amount of time that passes each frame - `dt`. The small change in momentum, defined by `dp` is simply the force vector multiplied by `dt`, the time interval. Once again, we use `dt` here because it scales the simulation to real time no matter what the frame rate of our virtual universe is set to.

Again, we define the change in velocity that the particle will experience based on its mass property. We divide the change in momentum by the particle's mass, like this:

```text
# Calculate the change in velocity
dv = dp / ball.mass
```

Then the next step is to interatively add `dv`, updating the velocity each frame:

```text
# Update the ball's velocity
ball.v = ball.v + dv
```

Once again, it is important to remember that this line of code should be read like this:

**"The new value of the ball's velocity is assigned to the old ball's velocity plus a small change in the velocity that ocurred in this frame."**

We just use the same iterative calculation process that we have used before:

```text
# Update the ball's position
ball.pos = ball.pos + ball.v * dt
```

Once again, this is assigning a new value for the position by adding a small amount of position change to the old position.

When you play the simulation, you should see the Particle accelerate in the negative direction.

## Analayze The Motion

You should once again create a motion graph to see if the virtual particle's motion is similar to a real object's motion based on our observations earlier in the year. Go ahead and create four graphs in the **Initial State** pane, two for analyzing the X and Y positions, and then two for analyzing the X and Y velocities:

```text
# Define some graphs
g_xpos = Graph("X Position vs Time")
g_ypos = Graph("Y Position vs Time")
g_vx = Graph("X Velocity vs Time")
g_vy = Graph("Y Velocity vs Time")
```

Once you have created the graphs, go to the **Calculations** pane and plot the points:

```text
# Plot the positions and velocities
g_xpos.plot(t, ball.pos[X])
g_ypos.plot(t, ball.pos[Y])
g_vx.plot(t, ball.v[X])
g_vy.plot(t, ball.v[Y])
```

Once you plot some points, make sure that graphs match your expectations...

## Curved Path Motion

Now that we have a particle whose state of motion is only being affected by gravity, its time to give the particle a non-zero velocity. Let's give it an initial velocity in the X direction. Go ahead and change the velocity to this:

```text
ball.v = [40, 0]
```

Then start the simulation again. What has happened to the behavior of the particle's motion? I hope you see that the Particle is moving along a curved path now...but why? It will be easier to see the dynamics involved here if we draw the particle's velocity vector. Add this line of code to the **Calculations** pane:

```text
drawArrow(ball.pos, ball.v, "green", true, 3)
```

The value of _true_ after the color green in the above line of code tells Tychos to display the component vectors of the arrow. The number 3 just makes the arrows a bit thicker so that we can see them more easily. When you play the simulation again you should see that the arrows for the vertical and horizontal velocities are behaving differently. Think about these questions:

* Which one is changing, and which one isn't?
* Why are they behavng this way?
* Why does this cause the ball to move along the cirved path that it is moving along?

Now, let's change the vertical velocity component so that it is intially moving in the positive vertical dimension. Once again, change the line of code for defining the initial velocity of the particle:

```text
ball.v = [40, 60]
```

When you play the simulation again, you will see that it moves upward first this time, but eventually arcs downward. Look at the graphs now. Notice the shapes of the graphs. Are these similar or different from the graphs we saw in LoggerPro? 

## Conclusion

This was a brief but important tutorial on how to simulate a projectile. Once again, we use the momentum principle and with just a few changes to a few lines of code, we can simulate a real object like a ball being thrown into the air. Here are the steps required to simulate a projectile

1. Define a gravitational force acting on a particle as a vector of \[0, -9.8\] multiplied by the mass of the particle.
2. Define the change in momentum using the momentum principle and the fact that the duration of time is defined by `dt`.
3. Give the particle an initial velocity in the X and Y directions.
4. Update the velocity based on the change in velocity caused by the change in momentum.
5. Update the postition using the updated velocity.



