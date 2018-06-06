# Lesson 5: Using Motion Graphs

## Lesson Objectives and Overview

Motion graphs are a powerful analytical tool. In this lesson students will learn how to create motion graphs for analyzing motion in Tychos.

* Students will learn how to create a Graph object with a title.
* Students will learn how to plot points on the graph in a specific color.
* Students will learn how to plot multiple data sets on a graph.
* Students will learn how to create multiple graphs.

You may have already seen motion graphs for position vs time in your Physics class where the position points are plotted on the vertical axis and the time values are plotted on the horizontal axis. Now you are going to learn how to do this in the simulation tool, Tychos.

Click on the link below to open the Tychos scenario in a new broswer tab where you can follow along, or use the embedded frame that contains the scneario below:

[Motion Graphs in Tychos](https://tychos.org/scenarios/388)

In order to display a motion graph, you must first create a particle and get it moving. We are going to create a Particle called `buggy1` that represents one of those nifty red constant velocity buggies that you may have used in class. Let's create that Particle in the **Initial State** pane:

```text
buggy1 = Particle([0, 50], 5, "red")
```

Lets give it a velocity only in the X direction for now. Add this line of code just below the one you wrote:

```text
buggy1.v = [10, 0]
```

The buggy won't move yet because we haven't told Tychos how to move it, but we will do that soon. 

## Adding A Graph

First, you are going to create a **graph** "object". This is done by typing this command in the **Initial State** pane:

```text
g_xpos = Graph("Name of your graph")
```

The above code creates a graph titled "Name of your graph". It is wise to actually have the graph title reflect what it is that you are actually going to plot. In our case it is the "x" position coordinate \(dependent variable\) versus the time \(independent variable\), so go ahead and change the title of the graph now:

```text
g_xpos = Graph("X Position vs. Time")
```

OK, this changes the title, but notice that the graph is blank. Nothing is actually being plotted. To tell the simulation tool to plot points, we have to tell it what to plot on each axis. 

## Plotting Points

Before we begin plotting points, let's make sure that the Particle - `buggy1` - is actually moving. Go to the **Calculations** pane and add this line of code:

```text
buggy1.pos = buggy1.pos + buggy1.v * dt
```

This will get `buggy1` moving and now we can plot its position as a function of time.

To plot points on your graph, you need to give it some coordinate points. Because we created a variable called `g_xpos` to represent our graph, we can now tell our graph to plot some points. The basic syntax looks like this:

`g_xpos.plot(independent variable, dependent variable)`

Just as in the experiment with the motion detector, the simulation tool can plot points for position as a function of time. Time is our independent variable, which is represented by the variable `t`. The X position of the buggy is our dependent variable. But just as was the case with LoggerPro, for a single plot, we can only plot a single dimension per plot command. The problem with this is that the particle's position is a matrix - it is inherently two dimensional. So for example, this code won't work:

```text
# this won't work!
g_xpos.plot(t, buggy1.pos)
```

We can access just the X or Y dimensions of a particle's position using this syntax:

```text
# plot just the x position
g_xpos.plot(t, buggy1.pos[X])
```

The `plot` command always needs to be placed in the **Calculations** pane because it is actually a repetitive calculation that the simulation tool must perform each frame.

When you run your simulation, you should see that the blank graph should suddenly look similar to this image below:

![Image](https://srcs.instructure.com/courses/1059/files/59832/download)

The program places a plotted point based on the rate identified by the slider labled **Graph Plot Interval** in the **Settings** tab. Decrease the interval to see more plotted points, and increase the interval to see less points.

### Changing The Plotted Point Colors

Its quite easy to change the colors of the plotted points, you just need to add a color name when you execute the plot command. Change the last line of code so that it looks like this:

```text
# Now plot some points...
g_xpos.plot(t, buggy1.pos[X], "red") 
```

### Multiple Plots

You can plot multiple sets of points on one graph. For example, maybe you wanted to plot the X position of another particle - maybe a second buggy...

In the **Initial State Pane**, go ahead and create another particle - let's say its called **buggy2**. The code in your **Initial State Pane** should now look like this:

```text
# A second buggy
buggy2 = Particle([100, 0], 5, "blue")
buggy2.v = [-20, 0]
```

This defines a second buggy that is blue and that is moving at let's say 20 cm/s. We just now need to model its movement like the first buggy. Add the code in the **Calculations Pane** so that we are updating the position of the second buggy `buggy2` using its velocity like this:

```text
buggy2.pos = buggy2.pos + buggy2.v * dt

```

Now that we have done that, we just need to add a second set of plotted points. Add this line of code to add those points to the same graph:

```text
g_xpos.plot(t, buggy2.pos[X], "blue")
```

You should now see two sets of points, one red and one blue, being plotted on the graph. You should notice something right away. If the red points were connected in a line and the blue points were connected in a line which would have a steeper slope? Which one has a negative slope? Does this match what you have learned about motion graphs? 

### Making Multiple Graphs

It is very easy to create multiple graphs. You simply have to add a second graph by defining a new variable, much like we do when we create a second particle. To add a new graph, simply add one more line to the **Initial State** pane:

```text
g_ypos = Graph("Y Position vs. Time")
```

The second graph is now identified by the new variable, `g_ypos`. How would you now plot the Y positions of the two particles on this new graph? Here are the remaining goals you should try to achieve:

* **Change the velocity of buggy1 so that the Y component is negative 10.**
* **Change the velocity of buggy2 so that the Y component is positive 5.**
* **Plot the position values of the two buggies Y positions on the graph in "red" and "blue" for the corresponding buggies.**

You should notice that the slopes of the plotted points in the Y position graph are different because these lines represent the positions of the particles in the Y dimension. One thing you shoud also notice is that the lines cross, showing you that the Y positions of the particles are shared at a point in time. Is there an intersection for the X position graph too? Notice the time at which the intersection point occurs.

## Conclusion

You should now be able to:

* Create a graph with a title,
* Plot points on the graph in different colors,
* Plot more than one set of points on a graph,
* Create multiple graphs.

Its now time to use Tychos to help you solve a problem in the real world...

