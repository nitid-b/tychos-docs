# Lesson 1: Introduction to Coding in Tychos

## Lesson Overview and Objectives

This lesson is a great place to start, and will help your students get acquainted with Tychos quickly.

* Students will learn how to navigate the Tychos interface.
* Students will learn how to create, use and modify comments, variables and built in functions.
* Students will learn about matrices and how to perform basic calculations \(add, subtract\) with matrices.

> Simulation is the [imitation](https://en.wikipedia.org/wiki/Imitation) of the operation of a real-world process or system over [time](https://en.wikipedia.org/wiki/Time).[\[1\]](https://en.wikipedia.org/wiki/Simulation#cite_note-definition-1) The act of simulating something first requires that a model be developed; this model represents the key characteristics or behaviors/[functions](https://en.wikipedia.org/wiki/Function_%28engineering%29) of the selected physical or abstract system or process. The model represents the system itself, whereas the simulation represents the operation of the system over time.

_-Wikipedia_

Scientists and engineers create computer simulations that allow them to create virtual universes so that they can better understand the real universe. If the virtual universe behaves similarly to the way nature behaves, then scientists can assume that their simulation is built on similar rules - what we call a model.

The simulation tool that you will be using throughout this course will help you test your understanding of the real world, and will even lead to discoveries about how the real world works.

## Coding Your Simulations

In order to build a simulation, you will first need to learn how to tell the underlying interpreter what you want your simulation to do. This requires learning the _programming interface_ of the tool.  A programming interface is essentially the language that the tool understands. Although this is not a computer programming course, you will be learning how to write some "code" that can be understood by the software that underlies the entire tool. When you write this code, you will be essentially writing a program that is executed by the simulation tool.

We are going to start slowly by covering some programming terminology that you will need to be familiar with to start creating simulations. Follow this guide below to help you familiarize yourself with some of the basic commands and syntax of the tool's programming interface.

## The Tychos Environment

Click on the link below to open the Tychos scenario in a new browser tab where you can follow along, or use the embedded frame that contains the scenario below:

{% embed data="{\"url\":\"https://tychos.org/scenarios/13\",\"type\":\"link\",\"title\":\"Tychos – Hackable Simulations\",\"icon\":{\"type\":\"icon\",\"url\":\"https://tychos.org/favicon.ico\",\"aspectRatio\":0}}" %}

### The Simulation "Hack" Panels

To get started, you will need to click on the little wrench at the top left corner of the window below. This reveals several tabs, each with its own purpose.

#### **Description Panel**

This is the description of the simulation, as well as any optional directions that can be identified by the simulation author.

![](https://tychos.org/static/help/ui/ui_desc_panel.png)

#### **Goals Panel**

The instructor or whoever wrote the scenario may include specific goals that the student should accomplish with this Scenario. Each goal has a description such as "Make particle p1 move to the right" and the goal will turn green when your program achieves that goal.

![](https://tychos.org/static/help/ui/ui_goal_panel.png)

#### **Initial State Panel**

You program the initial conditions of the simulation, e.g. creating particles, setting their initial position, creating graphs to view particular aspects of your simulation, and perhaps defining initial values such as the gravity or mass. The code that you write appears on the left of the screen, while each line of code is evaluated and its output appears on the right in blue text.

![](https://tychos.org/static/help/ui/ui_is_panel.png)

#### **Calculations Panel**

In this panel, you write your program for calculating what the simulation does for every moment in time as the simulation runs - called a frame. E.g. for a simulation of particles moving in space, you might examine several particles and calculate a new position for them given their existing momentum. Just as in the **Initial State** pane, the code that you write appears on the left of the screen, while each line of code is evaluated and its output appears on the right in blue text.

![](https://tychos.org/static/help/ui/ui_calc_panel.png)

#### **Settings Panel**

This pane allows you to change several settings of the simulation:

![](https://tychos.org/static/help/ui/ui_settings_panel.png)

* A button for displaying or hiding a **Motion Map**
* A slider for adjusting the _interval duration._
* A slider for adjusting the motion map's strobe rate.
* A slider for adjusting the plot rate for your graphs.
* An input box for setting the amount of time the simulation runs. A value of -1 tells the simulation to run indefinitely.
* There are several settings for adjusting how the World View is displayed. The World View window can either scale automatically depending on the space inhabited by any particles, or it can be set to a specific viewing size.

## Code Syntax

To get started writing some code, you are going to need to go to the **Initial State** pane.

Computers speak in languages that are very specific and precise. In order to communicate with a computer, we need to follow very specific rules.

### Writing Comments

Comments are really statements that are ignored by the computer. That might seem strange. Why would you use them? Well, this can be a handy way to put notes that can help describe what your code is doing because \(as you will see\) sometimes it is not obvious what a line of code is doing. Comments are also used to help others read your code. To identify a comment, you simply place a `#` character in front of the line:

```text
# This is a comment.
```

The second line of code will actually break the simulation engine. The software won't understand that second line of code, generating an error message. We will talk in more detail about how to interpret these errors later. For right now, just know that you can't communicate with the software using normal human speech - you are restricted to using the rules of language that the tool uses.

### Creating Variables

Just like in your Algebra class, the simulation tool can understand and use variables that are symbols whose value can change. To define a variable and give that variable a value you simply can type:

```text
x = 1
```

This defines a variable named `x` that initially has a value of `1`. You can define more than one variable as well:

```text
# This is one variable
x = 1

# This is another variable
y = 1
```

The variables above have the same value, but they can have different values.

### Using Simple Mathematical Operations

You can type simple calculations like the ones below, using the standard symbols for addition \(+\), subtraction \(-\), multiplication \(\*\) and division \(/\):

```text
# Basic math operations
1+1
2-5
3*2.5
5/2
```

These calculations get evaluated in the pane, and the resulting value is displayed on the right hand side of the pane in blue.

You can also use variables in your calculations like this:

```text
# Use a variable instead
x = 2
x+2
x-2
x*3
x/3
```

And you can even use different variables in the same calculations:

```text
# Use two variables instead
x = 2
y = 3
x+y
x-y
x*y
x/y
x%y
# Wonder what that last line does?
```

### Using Special Functions

There are some functions that are defined by the programming language that you can also use to do some more complex calculations. Here are just a couple, and we will learn more of these in the future:

```text
# This function computes the result of a base value raised to a power
pow(2,3)

# This function computes a square root
sqrt(16)
```

```text
# This function converts a degree value to a radian value
deg_to_rad(180)

# This function computes the sine of an angle in radians
sin(.57)
```

Notice in these lines of code that the function is defined by a name - like `pow` and `sqrt` and then you type an open parentheses "\(" and then the input values for the function, and then a closed parentheses "\)". The first function `pow` takes two inputs, the base and then the power. These are separated by a comma to identify the two inputs.

There are other functions that can be used to perform various calculations, and we will cover many of these this year. For a listing of others, you can check out the [Tychos Language Reference](../../getting-started/language-reference-api.md#other-useful-functions)

### Defining and Using Matrices

Being that we need to simulate 2 dimensional motion, then we need a way to represent two dimensional quantities in our simulated universe. Tychos allows you to represent two dimensional quantities by using a matrix form for vectors.

#### Defining A Matrix

For now let's just see how you define a matrix:

```text
# This is a two number (or element) matrix
m1 = [0,0]
```

As you can see above, you define a matrix by simply identifying the set of numbers inside two brackets "\[" and "\]" and then separate the numbers with a comma.

#### Matrix Calculations

The software allos you to perform various matrix calculations, very similar to the above calculations, but there are some important differences. Here are some ways in which you can perform calculations with a matrices:

#### **Adding, Subtracting, Multiplying and Dividing A Matrix and A Scalar:**

```text
# This is a two number (or element) matrix
m1 = [0,0]
# These are some simple calculations with a matrix
m1+2
m1-2
m1*2
m1/2
```

Can you see the pattern in the results? Notice how the calculation is performed on each number in the matrix. Now this gets really interesting when we start adding a matrix to another matrix.

#### **Matrix Addition and Subtraction:**

```text
# Here are two matrices
m1 = [1,2]
m2 = [2,1]

# Add and subtract matrices
m1+m2
m1-m2
```

#### Be Aware Of Some Matrix Oddities... 

Now, not all calculations work like this due to the underlying mathematical principles that define matrices. We won't go over these just yet, but it might interesting for you to try the following:

```text
# Here are two matrices
m1 = [1,2]
m2 = [2,1]

# Try this for some strange results...
m1*m2
```

Matrix multiplication is an advanced topic that we will cover soon. There are special matrix multiplication functions that we will discuss later.

#### Accessing An Individual Matrix Element

You can change a single value inside a matrix by accessing just that element. This is done by referencing the _index_ or position in the matrix. So for example, to change the first element in the matrix, you simply type:

```text
m1 = [0,0]
m1[1] = 2
```

Try this and look at the value of the matrix identified by the blue text and you will notice that it has indeed changed. Try changing the second element instead.

#### Working with Vectors in Polar Form

Often times, in physics and engineering, vector quantities can be represented in _polar form_ like this:

![LaTeX: \vec{s}\:=\:\left\(40\:m,\:120^\circ\right\)](https://srcs.instructure.com/equation_images/%255Cvec%257Bs%257D%255C%253A%253D%255C%253A%255Cleft%2840%255C%253Am%252C%255C%253A120%255E%255Ccirc%255Cright%29)

This would be a position vector that represents a distance of 40 meters pointing at a direction of 120 degrees.

There are two problems with vectors in this form. The first is that Tychos represents vectors as matrices, each element in a 2D matrix being equivalent to the X and Y components of the 2D vector. The second is that Tychos by default represents angles in units of radians, not degrees.

It might be useful to know how to convert a vector given to you in the polar form above to a matrix in Tychos. You can do that using some of the built in functions that are available.

To find the components, use these two lines of code:

```text
# X component:
x = 40*cos(deg_to_rad(120))

# Y component:
y = 40*sin(deg_to_rad(120))
```

The function _`deg_to_rad`_ converts the angle in degrees to radians. The _`sin`_ and _`cos`_ functions are the trig functions from math to give us the lengths of the "legs" of the triangle where 40 is the length of the hypotenuse.

You can also go the other way if you wish. Let's say that you have a vector in matrix form and for some reason you would like to see the length and heading of that vector. You can use some other built in functions to assist:

```text
vec = [10, 5]

# Find the length
m = mag(vec)

# Find the heading
angle = atan(5/10)
```

Above we used the function _mag_ that gives us the length of a vector and we used the _`atan`_ function which is the arc tangent function from trigonometry.

## Conclusion

You should now be able to:

* Write comments into your code.
* Create variables and give them values.
* Perform basic calculations with variables and values using operators and functions.
* Create 2D matrices and perform basic arithmetic calculations with those matrices.

