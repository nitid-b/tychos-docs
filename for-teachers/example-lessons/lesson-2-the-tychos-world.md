# Lesson 2: The Tychos World

## Lesson Overview and Objectives

In this lesson, students learn two of the important constituents of the Tychos world, namely the Particle object, and how to add vector arrows to visualize matrix quantities.

* Students will learn how to create Particles in Tychos - the basic constituent of any Tychos simulation.
* Students will learn how to use the function `drawArrow()` to represent position vectors for a Particle.

Click on the link below to open the Tychos scenario in a new browser tab where you can follow along, or use the embedded frame that contains the scenario below:

[Introduction to Particles](https://tychos.org/scenarios/14)

Now its time to actual simulate something in the simulated environment, and we are going to define the simplest, most basic object of our simulation - the particle.

You are going to learn today how you can create simulated particles in Tychos and how you can place those particles at different positions within the simulated 2D space.

## Creating Particles

To create a particle in the simulation, you need to first identify a valid variable name to store the reference to the particle. You then assign the variable to the result of a command that _invokes_ or essentially brings a particle into existence:

```text
p1 = Particle([0,0])
```

The command, or function called **Particle** requires one input in order to create a particle - a matrix that represents the position of the Particle. This particular particle is created and placed in the virtual world at the position of x = 0 and y = 0.

You can also define the size of the particle, but keep in mind that the size of our particle is really just for visual illustration and does not actually have any "physical" meaning in our virtual world because particles always exist at only a single point in space. Here is how you change the size:

```text
p1 = Particle([0,0], 10)
```

This changes the visual size of the particle on the screen, but doesn't actually change the fact that the particle only truly exists at x = 0, and y = 0.

You can also change the color of a particle. This can be helpful when you have multiple particles in your simulation and you want to be able to track certain particles visually on the screen. Below is an example of some of the colors that you can use:

```text
p1 = Particle([0,0], 10, "red")
```

Or...

```text
p1 = Particle([0,0], 10, "blue")
```

There are other colors that you can use, but I'll let you discover those on your own...

You can create more than one particle, you just have to assign it a different variable name. The code below creates two different particles. The names that you use can be almost anything:

```text
g_car = Particle([0, 100], 10, "green")
r_car = Particle([100, 0], 10, "red")
```

These might be two different partciles one representing a green car and another representing a red car.

### The Position Attribute

You can change the position of a particle variable by referencing its "pos" attribute. This is done by using a common computer science notation called "dot" notation. Its quite easy:

```text
p1.pos = [100, 0]
```

This line of code is read "The particle _p's_ position is now x = 100 and y = 0".

This ends the introductory lessons for orienting you to the simulation tool that we will be using frequently to help us discover the scientific models that best describe and predict nature's behavior.

## Visualizing Vectors

Tychos does have a tool for allowing us to draw vector arrows - its a function called  `drawArrow.` The `drawArrow()` function draws an arrow and is commonly used to illustrate vectors for many different kinds of vector quantities such as velocity, force etc. The function `drawArrow()`  should be called in the Calculations editor because it only draws the arrow for the current frame. If you call `drawArrow()` in the Initial State editor, you will not see anything.

The syntax for using this function looks like this:

```text
drawArrow([0, 0], [10, 10], "green")
```

This will draw an arrow that starts at the point \[0, 0\] and then extends to the point \[10, 10\] and is the color green. So the inputs for the function are as follows:

`drawArrow(pos, size, color, components)`

* `pos` — coordinates for the starting point of the arrow as an \[X,Y\] matrix.
* `size` — the vector to illustrate, e.g. \[10, 0\] will draw an arrow 10 units to the right.
* `color` — Optional color value for your arrow, e.g. "red" or an HTML value like "\#ff0000".
* `components` — Optional flag that determines if vector components are drawn, a value of `true` displays the components.

The second input, the size, should be seen as the actual size of the vector, not the end point of the vector. So for example, if you want to draw the vector \[10, 10\] but starting at the point \[0, 10\], notice that the actual tip of the vector extends to the point in space of \[10, 20\].

We can use this to visualize the position vector for a particle. This is done by using the position attribute as the vector to be drawn, and the origin as the starting point. You would draw a position vector for a particle called p1 using this code:

```text
drawArrow([0, 0], p1.pos, "green") 
```

...which will result in a vector arrow that points from the origin to the center of the particle on the screen.

You can also visualize the vector components by adding _true_ to the list of inputs in the _drawArrow_ function like this:

```text
drawArrow([0, 0], p1.pos, "green", true) 
```

This wil display the component vectors for the diagonal vector.

## Conclusion

You should now be able to:

* Create particles and give them a position, a size, and a color.
* Change the position of a particle.
* Draw vector arrows that represent 2D matrices.

