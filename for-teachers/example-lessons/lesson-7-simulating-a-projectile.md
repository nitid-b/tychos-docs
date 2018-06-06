# Lesson 6: Modeling The Momentum Principle

## Lesson Objectives and Overview

Students finally get to see how a force can be modeled in Tychos and how the change in a particle's state can be calculated using the momentum principle.

* Students will learn how to define a mass attribute for a particle.
* Students will learn how to calculate a change in momentum due to an applied force.
* Students will learn how to update a particle's velocity based on a change in momentum caused by the force.

The momentum principle is a very powerful principle that helps us understand the cause and effect relationship between forces acting on an object, and how that object's state of motion is changing. The momentum principle can be stated like this:

![LaTeX: \sum F\:\cdot\Delta t\:=\:m\cdot\Delta v](https://srcs.instructure.com/equation_images/%255Csum%2520F%255C%253A%255Ccdot%255CDelta%2520t%255C%253A%253D%255C%253Am%255Ccdot%255CDelta%2520v)

The idea communicated in this simple formula is that the sum of all forces acting on an object for an interval of time will cause the object to experience a change in velocity. It also states that the larger the mass of the object, then the smaller the change in velocity over that interval of time.

Forces are vectors, just like velocity, and therefore they exist in more than one spacial dimension. They have direction as well as magnitude. We are going to need to modify the above formula to represent these values as vectors:

![LaTeX: \sum \vec{F}\:\cdot\Delta t\:=\:m\cdot\vec{\Delta v}](https://srcs.instructure.com/equation_images/%255Csum%2520%255Cvec%257BF%257D%255C%253A%255Ccdot%255CDelta%2520t%255C%253A%253D%255C%253Am%255Ccdot%255Cvec%257B%255CDelta%2520v%257D)

Although this might seem like a small change, it is a very important one.

In this tutorial we will investigate how to simulate a force as a 2D vector that acts on a particle, and then we will consider how a simulated particle behaves when acted upon by more than one force.

## Simulating A Force

To follow along in this tutorial, open the scenario in a new tab by clicking on the link below:

[Simulating The Momentum Principle](https://tychos.org/scenarios/391)

The first thing that you are going to need to do is create a particle that we can apply our force on. For review, see if you can remember how to do this by achieving this goal:

* **Create a particle called "ball" with an initial position of \[0, 0\] and a radius of 5."**

Once you have done this, your goal will not turn green. You have to continue with the tutorial to learn something new...

The next step in the **Initial State** pane is to give the ball a velocity that is \[0, 0\] like this:

```text
ball.v = [0, 0]
```

To define a force, all we need to do is to define the magnitude of the force in each dimension using a matrix. We can simply define a matrix variable in the **Initial State** pane, just as we would any matrix variable:

```text
# Define a 2D force as a matrix
force1 = [10, 0]
```

In order for the particle to respond to the force defined by the momentum principle, the particle must have a mass. Just as we defined a velocity property for a particle, we can define a mass property. Remember, Tychos has no idea what mass is, it will be up to us to tell Tychos how to update the position of the particle based on some mathematical calculation that will be dependent on this new property that we are defining here. Add this line of code to the **Initial State** pane:

```text
# Define a mass property and give it a value
ball.mass = 10
```

This new property will be used in the **Calculations** pane.

## Updating The Velocity

We are ready to do some calculations so that we can define the behavior of the particle based on the applied force we defined above. Click on the **Calculations** pane because that is where we need to write the rest of our code.

Based on the momentum principle, a force applied for an interval of time will affect the momentum of a particle. We can therefore define a change in momentum in code like this:

```text
# Define a change in momentum
dp = force1 * dt
```

The interval time is of course the amount of time that passes each frame - `dt`. The small change in momentum, defined by `dp`is simply the force vector multiplied by `dt`, the time interval. Once again, we use `dt` here because it scales the simulation to real time no matter what the frame rate of our virtual universe is set to.

We can calculate the change in velocity that the particle will experience based on its mass property. We divide the change in momentum by the particle's mass, like this:

```text
# Calculate the change in velocity
dv = dp / ball.mass
```

The variable `dv` represents the change in velocity that will occur in one frame. We need to then add this value to the current velocity value so that it is updated. Again, remember that Tychos will do this iteratively, updating the velocity each frame as long as the calculation is indeed in the **Calculation** pane:

```text
# Update the ball's velocity
ball.v = ball.v + dv
```

Once again, it is important to remember that this line of code should be read like this:

**"The new value of the ball's velocity is assigned to the old ball's velocity plus a small change in the velocity that ocurred in this frame."**

## Update the Position

Now that we have the new velocity of the `ball` we can use that value to calculate the new position that `ball` should move to in the animation. We just use the same iterative calculation process that we have used before:

```text
# Update the ball's position
ball.pos = ball.pos + ball.v * dt
```

Once again, this is assigning a new value for the position by adding a small amount of position change to the old position.

When you play the simulation, you should see the Particle accelerate as its momentum is changing because of the force interaction we modeled. Stop the animation, then change the `mass` of the `ball` and then replay the simulation to see how the `ball` changes its behavior. Is it acting as you would expect?

## Analayze The Motion

You should create a motion graph to see if the virtual particle's motion is similar to a real object's motion based on your observations of real objects. Go ahead and create four graphs in the **Initial State** pane, two for analyzing the X and Y positions, and then two for analyzing the X and Y velocities:

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

Once you plot some points, you should see that the velocity graphs are linear while at least one of the positions graphs is curved...Does this match your expectations?

Before moving onto the next section, you should try to accomplish the following goals because they will ask you to create a different Particle that is acted upon by a force that has both an X and a Y component:

* **Create a new Particle called "ball2" that begins at \[0, 30\], has a radius of 5, a mass of 5.**
* **Define a force called "force2" whose value is \[5, 5\].**
* **Apply the force on "ball2" using the Momentum Principle to change its velocity.**

HINT: In order to do the above, you are going to need to define a new dp2 and dv2 representing the new change in momentum and change in velocity for particle 2.

## Simulating Multiple Forces

Now that you have learned to model a force acting on a Particle, its time to look at how we can model the behavior of a Particle when more than one force acts on it. As we stated earlier in this tutorial, forces are vectors. This means that when forces are added together, we have to consider that they are now vector quantities and not just scalars:

![LaTeX: \sum \vec{F}\:=\:\vec{F\_1}+\vec{F\_2}+\vec{F\_3}+...](https://srcs.instructure.com/equation_images/%255Csum%2520%255Cvec%257BF%257D%255C%253A%253D%255C%253A%255Cvec%257BF_1%257D%252B%255Cvec%257BF_2%257D%252B%255Cvec%257BF_3%257D%252B...)

That means that everything that we have learned about vectors applies here when we are calculating the net force on an object. The magnitude AND the direction of each force matters when we add the vectors together.

We are going to apply a new force to our original Particle called `ball`. This new force will be called `force3`. Add this line of code to the **Initial State** pane:

```text
# Define a new force called force3
force3 = [-5, 5]
```

This is all that needs to be done in the **Initial State** pane. Click on the **Calculations** pane because that is where we need to modify some of the code that we wrote earlier. In the previous section of this tutorial, we defined the change in momentum for the `ball` Particle using this line of code:

```text
# Define a change in momentum
dp = force1 * dt
```

The problem with this is that we now have more than one force acting on the Particle. The `ball` Particle's momentum will be affected by the NET force, the sum total of all forces acting on it. We can simply modify this line of code so that it now looks like this:

```text
# Define a change in momentum
dp3 = (force1 + force3) * dt
```

When you start your simulation, you should see the `ball3` Particle accelerate along a diagonal path because two forces are acting on it now, not just one.

You can also define a new variable that is simply the net forces acting on `ball3.` We do that below by defining a new variable called `Fnet3` that represents all the forces combined:

```text
# Define a net force
Fnet3 = (force1 + force3)

# Define a change in momentum
dp3 = Fnet3 * dt
```

Obviously this is an optional step, but it can help when reading the code to define variables that represent quantities that we define in Physics.

The following goals will test if you can model multiple forces acting on a Particle:

* **Create a new Particle called "ball3" that begins at \[100, 0\], has a radius of 5, a mass of 10 and any color you like.**
* **Apply all three forces \("force1", "force2" and "force3"\) on "ball3" using the Momentum Principle to change its velocity.**

{% hint style="info" %}
Once again, in order to do the above, you are going to need to define a new `dp3` and `dv3` representing the new change in momentum and change in velocity for particle 3.
{% endhint %}

As a last step, lets analyze the motion of the `ball3` just a little more closely. Change these lines of code in the **Calculations Pane** from:

```text
# Plot the positions and velocities
g_xpos.plot(t, ball.pos[X])
g_ypos.plot(t, ball.pos[Y])
g_vx.plot(t, ball.v[X])
g_vy.plot(t, ball.v[Y])
```

To:

```text
# Plot the positions and velocities
g_xpos.plot(t, ball3.pos[X])
g_ypos.plot(t, ball3.pos[Y])
g_vx.plot(t, ball3.v[X])
g_vy.plot(t, ball3.v[Y])
```

It should reveal something interesting. The object is accelerating in each of the dimensions, and so there really is a kind of independence of motion as it exists in each dimension without affecting the other. If you were to change one of the X components of one of the forces, it would only change the behavior of the particle's motion in that dimension. This is a powerful idea that we will return to...

## Conclusion

This was a brief but important tutorial on how to simulate forces. Hopefully you can see that will a few lines of code that model the Momentum Priniciple calculations, we can simulate particles accelerating in our 2D universe. Here are the steps required to simulate a force on a Particle

1. Define a force variable as a vector.
2. Define a mass attribute for a Particle. This is done by simply using the "dot" notation and giving the attribute a value.
3. Define the change in momentum using the momentum principle and the fact that the duration of time is defined by `dt`.
4. Update the velocity based on the change in velocity caused by the change in momentum.
5. Update the position using the updated velocity.



