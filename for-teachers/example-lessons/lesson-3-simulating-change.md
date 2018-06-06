# Lesson 3: Simulating Change

## Lesson Objectives and Overview

Now that students know the basics of writing code in Tychos, its time to learn about coding repetitive calculations - what is known as iterative calculations. This is essential before moving on to simulating motion.

* Students will learn how change the value of a variable each frame.
* Students will learn how to use the built in variables of `t` and `dt` to represent time.
* Students will learn how to scale their calculations from frame rate time in Tychos to seconds using `dt`.

## Real Time vs Virtual Time

Before we begin discussing how to simulate motion in 2 dimensions, we have to talk about time. All motion presupposes the existence of time, and so we must define the concept of time in our simulation tool.

Click on the link below to open the Tychos scenario in a new browser tab where you can follow along, or use the embedded frame that contains the scenario below:

[Executing Repetitve Calculations](https://tychos.org/scenarios/337)

In our simulated universe, time progresses as a function of what is known as the _frame rate_. This is the rate at which the universe recalculates the positions of all objects in the universe and then updates \(or "refreshes"\) the universe. Each frame represents an individual calculation and "still frame" of the universe. It is a "step" in the evolution of the universe. Tychos uses a number of variables that each represent time in slightly different ways. Understanding each one is important to understanding how Tychos works.

Type the following into the **Calculations Pane**:

```text
# The time interval
dt

# The number of elapsed frames
frame_count

# Time elapsed in seconds
t
```

When you start the simulation, you should see in the blue text on the right side of the pane the values for each variable. To slow down the numbers that are changing, you can click the **Step** button at the bottom of the simulation world window. Each time you click this button, you should see some of the numbers change.

Notice that `dt` does not change. This is the interval time - the segment of time between each frame. It is the "time step", or "delta time" that is used to calculate the amount of change that occurs from frame to frame. The smaller the value of `dt`, then the more frames per second that will be calculated for the animation. This will result in a smoother animation.

You will see that the value of the next two variables are changing quickly. They are both increasing. The `frame_count` is the number of frames that have elapsed since you pressed the start button. This value represents the number of time intervals that have elapsed, and thus the number of times the universe has been updated. The varialbe `t` is actually the time in seconds that have elapsed since you pressed the start button. Type the following line of code into the **Calculations** pane:

```text
frame_count * dt
```

Notice what this calculation returns as an output shown in the blue text. This demonstrates that the elapsed time in seconds is equal to the number of frames so far in the animation multiplied by the time interval between each frame. Each frame represents the state of our universe _at that moment in time_ and the frame rate is rate at which our simulated universe evolves.

You can modify the rate at which your universe evolves, and how _smoothy_ or accurately it evolves. This is done by going to the **Settings Pane** and adjusting the **Interval Duration.** Setting the interval duration low can result in slow animations because the number of times the universe has to be updated increases for each second, but setting it too high can cause the animation to "jump" and become less accurate. Change this setting and watch how the variable `frame_count` and `dt` change.

## Repeating Calculations

One of the powerful aspects of computers is their ability to repeat calculations, and also to use a previous calculation as an input for the next calculation. For example, we can ask the computer to continually add one to a variable, thus increasing its value every time a new frame _passes._ In the **Initial State** pane, let's create a new variable:

```text
x = 0
```

Then in the **Calculations** pane, type the following line of code:

```text
x = x + 1
```

This might seem like an odd line of code.

A very important point needs to be made here. The above line of code is not saying that "x" is equal to "x" plus one. That would be impossible mathematically because if "x" were 2, then how could 2 = 2 + 1?! In most computer programming languages though, the "=" sign is not a statement of equality, but rather a way to assign an new value to a variable - its an _assignment operator_. So the code actually is saying this: 

_"Assign a new value to x that is the old value of x plus one"._

When you run the simulation, notice what is happening to the blue text.

The value of of the calculation is changing because with every frame, the value of **x** has changed from the previous calculation. This is because we aren't just doing a calculation, but we are also reassigning the value of **x** to the value of the old "x" plus 1. So if "x" were 2, then the next frame "x" will be now 3 - its old value of 2 plus 1, making its new value 3.

There are a couple of goals you should try to achieve in the scenario just to make sure that you get how this works: 

* **Create a variable called y whose initial value is 100 but that decreases by 1 each frame.**
* **Create a variable called z whose initial value is 0 but whose value is always the result of y divided by x.**

### Recurring Matrix Calculations

Just like normal variables, matrix variables can be involved in recurring calculations. It is very similar, you just need to remember to perform the calculations as well as reassigning the result back to the original variable. There are several ways to do this, but let's look at the easiest to understand.

First create this new matrix variable called `m1` in the **Initial State Pane**:

```text
m1 = [0, 0]
```

We are gong to use the incrementing value for `x` that we used before. Now assign the first element in the matrix to the value of `x`. This is done in the **Calculations** pane:

```text
x = x + 1
m1[1] = x 
```

When you run your simulation you should notice that the value of the matrix changes.

You could also simply add an incremental matrix - a "change" matrix like this:

```text
m1 = m1 + [1, 1]
```

Just like with a single value, the matrix `m1` will change in value by \[1, 1\] so each of the elements in the matrix will increment by 1 every frame.

Try creating some matrices whose values change each frame by achieving the next two goals:

* **Create a variable called m2 whose initial value is \[100, 100\] but that decreases by \[1, 1\] each frame.**
* **Create a variable called m3 whose initial value is \[0, 0\] but whose value is always the result of m1 + m2.**

## Using Meters To Display Variable Values

Tychos provides a way for you to more easily see in the simulated world a variable's value. This tool is called a `Meter`. A `Meter` is a numeric display that you create in the **Initial State Pane** and then you specify the data to display in the **Calculations** **Pane**. Each `Meter`  that is created will appear on the left side of the World View. Your program needs to tell the `Meter` what value it needs to display by using the `read` command.

To create a  `Meter` , you first need to write this line of code in the **Initial State Pane**:

```text
mx = Meter("Value for x")
```

This tells Tychos to create a new display box in the World View with the title "Value for x".

To get the  `Meter` to actually display data, you need to specify a numeric variable's value to  `read` . This line of code would need to be written in the **Calculations Pane**:

```text
mx.read(x)
```

This would then allow the  `Meter` to read the value of the variable  `Meter` and display it on the screen. You can only read a non-matrix value to a  `Meter` , so if you want to display a matrix value you can only display one element of the matrix using this notation:

```text
# Display element 1 of a matrix m1 
mx.read(m1[1])

# Display element 2 of a matrix
mx.read(m1[2])
```

## Scaling Time to Seconds

This next point is very important to understand. So far all of our calculations were scaled to the frame rate, which is a unit of time. The unit of time that we use in our experiments is the second. In order for our simulations to be scaled to this "real time" in seconds, we need to do a _scaling_ calculation.

This point can be demonstrated. Let's suppose that you wanted to change a variable's value by a certain amount _each second_. For example, we wanted to change the value of a new variable, lets call it `s`, and we want to change the value of `s` by 10 each second. Create the variables in the **Initial State Pane**:

```text
s = 0
```

Now try this in the **Calculations Pane**:

```text
s = s + 10
```

What you should see is that the value of s is increasing way too quickly! That's because it is increasing by 10 every frame, not 10 every second! If the frame rate were 50 frames per second, then the value of `s` would already be 500 by the end of the first second!

Remember that each frame represents a time duration for the existence of the simulated universe - a "step" in its evolution. The time interval is represented by the variable `dt` and its value is based on a the number of frames that pass each second. If the frame rate were 50 frames per second, then the value of `dt` would be .02 because:

![LaTeX: dt\:=\frac{\:1s}{50\:frames}=.02](https://srcs.instructure.com/equation_images/dt%255C%253A%253D%255Cfrac%257B%255C%253A1s%257D%257B50%255C%253Aframes%257D%253D.02)

We can use this important variable to scale our calculation to a time based on seconds rather than a time based on frames. We are going to define a new variable called `ds` that will represent how much we want to change s _each frame_:

```text
ds = 10 * dt
```

The value of `ds` is:

![LaTeX: ds\:=\:10\cdot\left\(.02\right\)=.2](https://srcs.instructure.com/equation_images/ds%255C%253A%253D%255C%253A10%255Ccdot%255Cleft%28.02%255Cright%29%253D.2)

So if we perform this calculation for increasing `s`:

```text
s = s + ds
```

You will see that the value of `s` will increase by .2 each frame, and because there 50 frames in a given a second, then we can see that the value of s after a single second should increase by 10 because it increased by 0.2 fifty times in one second:

![LaTeX: 50\cdot\left\(.2\right\)\:=\:10](https://srcs.instructure.com/equation_images/50%255Ccdot%255Cleft%28.2%255Cright%29%255C%253A%253D%255C%253A10)

This allows us to perform calculations based on seconds rather than having to figure out how much to change our variables based on the frame rate. This is really good, because now, if we change the frame rate, the calculations do not have to be rescaled and thus our code does not have to change. You can test this out by changing the interval duration time in the **Settings** tab and you will see that the _rate_ of change to s remains the same. The only difference is how much it changes each frame, but not each second.

Try these goals to see if you fully understand this:

* **Create a variable called s2 whose initial value is 100 but decreases by a value of 10 each second.**
* **Create a variable called m4 whose initial value is \[0, 0\] but whose value changes by \[10, -5\] each second.**

We are now ready to start talking about how to simulate motion...

