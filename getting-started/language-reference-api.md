---
description: The following is a reference guide for the Tychos programming interface.
---

# Language Reference \(API\)

## Comments

Comments are statements that you can insert in your code that do not get interpreted and executed by Tychos. To create a comment, you simply indicate a comment by using a hashtag:

```text
# This is a comment.
```

## Variables

To define a variable in Tychos all you need to do is identify a name for the variable. You then type an `=` sign to assign a value to the variable. The following demonstrates various variable declarations

```text
# Assigns a variable called x the value of 10
x = 10

# Assign a new variable y the value of the x
y = x

# Assign x the value of itself plus 1
x = x + 1
```

## Built-in Scenario Variables

There are a few variables that are built into Tychos. These variables are:

* `t` — How many seconds has passed since this Scenario was started?
* `dt` — Time between frames as seconds, e.g. 0.1 is 1/10th of a second.
* `frame_count` — How many frames have passed? e.g. 1, 2, 3...
* `X`, `Y` — These are shortcuts for indexing the first two elements of 2-D matrices, e.g. `my_particle.pos[X]`

## Common Math Operators and Functions

These are some common mathematical operators and functions for performing various calculations.

### Mathematical Operators

Tychos uses the following operators to perform basic math calculations:

* `+` — Addition
* `-` — Subtraction
* `*` - Multiplication
* `/` - Division
* `^` - Exponent
* `%` - Modulo

### Basic Math Functions

You can also use the following basic math functions:

#### **pow\(base, power\)**

The `pow(base, power)` function takes two arguments, raising the `base` by the `power`.

```text
# returns number 8
pow(2, 3)
```

#### **sqrt\(positive\_number\)**

The `sqrt(positive_number)` function takes a single non negative number and returns the real square root of the number.

```text
# returns number 2
sqrt(4)
```

#### **abs\(number\)**

The `abs(number)` function returns the absolute value of a number.

```text
# returns number 2
abs(-2)
```

### Trigonometric Functions

The following functions all use radians as the angle measurement. You can use `pi` to represent PI.

#### **sin\(angle\)**

The `sin(angle)` function is used to evaluate the trigonometric sine value for a given input angle. The input angle must be provided in radians.

```text
# returns number 1
sin(pi/2)  
```

#### **cos\(angle\)**

The `cos(angle)` function is used to evaluate the trigonometric cosine value for a given input angle. The input angle must be provided in radians.

```text
# returns number 1
cos(0)
```

#### **tan\(angle\)**

The `tan(angle)` function is used to evaluate the trigonometric tangent value for a given input angle. The input angle must be provided in radians.

```text
# returns number 1
tan(pi/4)
```

#### **asin\(value\)**

The `asin(value)` function is used to evaluate the trigonometric arcsine value \(inverse sine\) for a given input. The output angle is given in radians.

```text
# returns number 1.57
asin(1)  
```

#### **acos\(value\)**

The `acos(value)` function is used to evaluate the trigonometric arccosine value \(inverse cosine\) for a given input. The output angle is given in radians.

```text
# returns number 0
acos(1)
```

#### **atan\(value\)**

The `atan(value)` function is used to evaluate the trigonometric arctangent value \(inverse tangent\) for a given input. The output angle is given in radians.

```text
# returns number .785
atan(1)
```

#### **deg\_to\_rad\(angle\)**

The `deg_to_rad(angle)` function is not part of the MathNotepad language but is provided as a helper function to make the conversion from degree angles to radians easier. The input is an angle measurement in degrees and the output is the angle measurement in radians.

```text
# returns number .785
deg_to_rad(45)
```

#### **rad\_to\_deg\(angle\)**

The `rad_to_deg(angle)` function is not part of the MathNotepad language but is provided as a helper function to make the conversion from radian angles to degrees easier. The input is an angle measurement in radians and the output is the angle measurement in degrees.

```text
# returns number 180
rad_to_deg(p1)
```

### Matrix Functions

The following functions provide operations for matrix calculations.

#### **dot\(x, y\)**

Calculates the dot product of two vectors. The dot product of `x = [a1, a2, a3, ..., an]` and `y = [b1, b2, b3, ..., bn]` is defined as:

`dot(x, y) = a1 * b1 + a2 * b2 + a3 * b3 + … + an * bn`

```text
# Work is the dot product of Force (F) and displacement (r)
F = [2, 2]
r = [3, 3]

# returns 12
Work = dot(F, r)
```

#### **cross**

Calculates the cross product for two vectors in three dimensional space. The cross product of `x = [a1, a2, a3]`and `y = [b1, b2, b3]` is defined as:

`cross(x, y) = [ a2 * b3 - a3 * b2, a3 * b1 - a1 * b3, a1 * b2 - a2 * b1 ]`

If one of the input vectors has a dimension greater than 1, the output vector will be a 1x3 \(2-dimensional\) matrix.

```text
# Torque is the cross product of Force and moment arm (r)
F = [2, 0, 0]
r = [0, 2, 0]
# returns matrix [0, 0, 4]
cross(F, r);
```

## Other Useful Functions

Some other useful functions...

#### **random\(min, max\)**

Return a random number larger or equal to min and smaller than max using a uniform distribution. If now min or max are given, then it returns a random value from 0 to 1. If just one value is given, then it returns a random number between 0 and the input value.

```text
random()       # returns a random number between 0 and 1
random(100)    # returns a random number between 0 and 100
random(30, 40)  # returns a random number between 30 and 40
random([2, 3])  # returns a 2x3 matrix with random numbers between 0 and 1
```

#### **drawArrow**

The `drawArrow` function draws an arrow and is commonly used to illustrate vectors for a particle. drawArrow should be called in the Calculations editor because it only draws the arrow for the current frame. If you call drawArrow\(\) in the Initial State editor, you will not see anything.

![](https://tychos.org/static/help/drawArrow_1.png)![](https://tychos.org/static/help/drawArrow_2.png)

`drawArrow(pos=[0,0], size=[1,0], color="black", components)` -&gt; returns and draws an Arrow object

* `pos` — coordinates for the starting point of the arrow as an \[X,Y\] matrix.
* `size` — the vector to illustrate, e.g. \[10, 0\] will draw an arrow 10 units to the right.
* `color` — Optional HTML color value for your arrow, e.g. "red" or "\#ff0000".
* `components` — Optional flag that determines if vector components are drawn, a value of `true` displays the components.

Example — The illustrations at right were drawn using these commands:

```text
# Initial State editor
p = Particle([0,0], 10, "green")

# Calculations editor
drawArrow(p.pos, [20, 20], "purple")        # just the diagonal arrow
drawArrow(p.pos, [20, 20], "purple", true)  # also draw X and Y components
```

#### **unit\_vector**

This function returns a unit vector representation of the given input vector. Its magnitude is 1 and the direction matches the direction of the input vector. This can be useful if you need just the direction of a vector, but not its magnitude.

`unit_vector(vec)` -&gt; returns a vector of length 1, and in same direction as `vec`.

* `vec` - any two dimensional vector as a \[X, Y\] matrix.

Example:

```text
u = unit_vector([3, 4])  # returns [0.6, 0.8]
magnitude(u)             # returns 1
```

#### **magnitude**

This function returns the scaler magnitude of any given vector. This is helpful when you want to know the length of a vector, for example, if you want the magnitude of a vector, but not its direction.

`magnitude(vec)` -&gt; returns the scaler magnitude of the vector `vec`.

* `vec` - any two dimensional vector as a \[X, Y\] matrix.

Example:

```text
magnitude([3, 4])             # returns 5
```

### Comparison Functions

The following functions are used to compare two values as being equal or unequal as well as testing if one value is larger or smaller than another. These are very helpful when writing goals for students.

#### **equal\(x, y\)**

The function tests if two values \(x and y\) are equal. It returns a boolean value of `true` or `false`.

```text
equal(2 + 2, 3)        # returns false
equal(2 + 2, 4)        # returns true
equal(t, 10)           # returns true if t is 10, or false if it is not.
```

#### **deepEqual\(x, y\)**

This function is similar to `equal`, but it tests element wise whether two matrices are equal. It returns a boolean value of `true` or `false`. The code below demonstrates the difference between `equal` and `deepEqual`:

```text
p1 = Particle([10, 10])
p2 = Particle([10, 0])

deepEqual(p1.pos, p2.pos)   # returns false
equal(p1.pos, p2.pos)       # returns [true, false]
```

#### **larger\(x, y\)**

The function tests if one value \(x\) is larger than another \(y\). It returns a boolean value of `true` or `false`.

```text
larger(2, 3)        # returns false
larger(3, 2)        # returns true
larger(2, 2)        # returns false
```

#### **smaller\(x, y\)**

The function tests if one value \(x\) is smaller than another \(y\). It returns a boolean value of `true` or `false`.

```text
smaller(2, 3)        # returns true
smaller(3, 2)        # returns false
smaller(2, 2)        # returns false
```

#### **unequal\(x, y\)**

The function tests if two values \(x and y\) are unequal. It returns a boolean value of `true` or `false`.

```text
unequal(2 + 2, 3)        # returns true
unequal(2 + 2, 4)        # returns false
unequal(t, 10)           # returns false if t is 10, or true if it is not.
```

Comparison operators return `true` or `false` but these also evaluate to 1 \(true\) or 0 \(false\). This can allow you to conditonally assign a value to a variable depending on the evaluation of the comparison. See the code below as an example:

```text
# If t is larger than 10, then the value of F is [10, 10], otherwise it is 0.
F = larger(t, 10) * [10, 10]
```

### Logical Operators

The following operators are used to execute logical AND and OR comparisons for the use of evaluating logical statements.

#### **and**

This is used for performing a logical AND conjunction. For example, "A and B" is true only if A is true and B is true. "A and B" is false if either A or B is false.

```text
A = true
B = true

A and B # returns true

B = false

A and B # returns false
```

You can use the `and` operator to test if two comparisons are both true:

```text
x = 2

smaller(x, 3) and equal(x, 2)  # returns true
smaller(x, 3) and unequal(x, 2) # returns false
```

#### **or**

This is used for performing a logical OR conjunction. For example, "A or B" is true if A or B is true. "A or B" is false only if A and B are both false.

```text
A = true
B = false

A or B # returns true

A = false

A or B # returns false
```

You can use the `or` operator to test if one of two comparisons are true:

```text
x = 2

smaller(x, 3) or equal(x, 3)  # one is true, so returns true
smaller(x, 1) or equal(x, 3) # both are false, so returns false
```

## Built-in Classes

Tychos has only a few classes that are used to create the basic simulated objects in the Tychos universe as well as a few tools for analyzing those objects in the simulated world. The two simulated objects in Tychos are the `Particle`and the `Block`. The tools that can be used for analyzing the behavior of your simulations are the `Graph` and the `Meter`.

### Particle

A `Particle` represents a spherical particle in the simulated world and is drawn as a colored circle in the World View. A particle has position, radius and color.

![](https://tychos.org/static/writing_scenarios/particle.png)

`Particle(pos=[0,0], radius=10, color=default_color)` -&gt; returns a Particle

* `pos` — The inital position of your particle in \[X,Y\] coordinates. If you don't specify a position, the default value of \[0,0\] is used.
* `radius` — The radius of the circle that is drawn in the World View to represent this particle.
* `color` — The particle will be drawn in this color. Use HTML colors e.g. "\#ff3300", "blue".

These attributes may also be modified on the particle after it is created. In particular, one will usually change the `pos` attribute of a particle in the Calculations editor to show a particle's movement. E.g.

```text
# Initial State editor
p = Particle()
p_big = Particle([50, 0], 25)
p_big.color = "red"
p_blue = Particle([100, 0], 10, "green")

# Calculations editor
p.pos = p.pos + [1, 0.25]
```

### Block

Another particle representation in Tychos is the `Block`. A `Block` is very similar to a `Partcle` but it is represented as a colored rectangle in the World View. A block has position, width, height and color. Just as with Particle's, Tychos only uses the width and height attributes for display. You can define how these attributes change given the rules of the simulation that you define.

`Block(pos=[0,0], size=[10, 10], color=default_color)` -&gt; returns a Block

* `pos` — The inital position of your block in \[X,Y\] coordinates. If you don't specify a position, the default value of \[0,0\] is used.
* `size` — The width and height of the block that is drawn in the World View to represent the block.
* `color` — The block will be drawn in this color. Use HTML colors e.g. "\#ff3300", "blue".

![](https://tychos.org/static/help/ref/ref_block.png)

These attributes may also be modified on the block after it is created. In particular, one will usually change the `pos` attribute of a block in the Calculations editor to show a block's movement. E.g.

```text
# Initial State editor
b1 = Block([0, 0], [10, 10], "green")
b2 = Block([20, 0], [10, 20], "blue")
b3 = Block([40, 0], [20, 10], "orange")

# Calculations editor
b1.pos = b1.pos + [1, 0.25]
```

### Graph

A `Graph` is a 2-dimensional chart of data that you specify in the Calculations editor. Each Graph that is created will appear on the right side of the World View. Your program needs to add points to the graph with the `plot`command.

`Graph(title="")` -&gt; Returns a Graph

* `title` = Optional text that will appear at the top of the graph.

#### **Graph.plot**

`graph.plot(x, y, color=default_color)` — Adds a data point to your graph.

![](https://tychos.org/static/writing_scenarios/graph.png)

Example:

```text
# Initial State editor
g = Graph("Graph with two points")
g_color = Graph("Graph with color")

# Calculations editor
g.plot(0, 0)
g.plot(10, 30)

g_color.plot(-10, 0, "red")
g_color.plot(20, 0, "red")
g_color.plot(0, 20, "blue")
g_color.plot(0, -30, "blue")
```

### Meter

A `Meter` is a numeric display of data that you specify in the Calculations editor. Each Meter that is created will appear on the left side of the World View. Your program needs to tell the Meter what value it needs to display by using the `read` command.

![](https://tychos.org/static/help/ref/ref_meter.png)

`Meter(title="")` -&gt; Returns a Meter

* `title` = Optional text that will appear at the top of the meter.

#### **Meter.read**

`meter.read(value)` — Reads the value and displays it on the Meter.

Example:

```text
# Initial State editor
mt = Meter("Time")
mx = Meter("X Position")
mv = Meter("X Velocity")

# Calculations editor
mt.read(t)
mx.read(particle.pos[X])
mv.read(particle.vel[X])
```



