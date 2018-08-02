# Lesson 8: Conditional Forces

## Lesson Objectives and Overview

Tychos has the ability to evaluate a condition based on a comparison between two values. This can be used to activate or deactivate a force given a specific condition. In this lesson students will learn about conditional statements and how they can be used to simulate a force that conditionally acts on an object.

* Students will learn how to define a conditional statement and use it to modify a varaible's value conditionally.
* Students will learn how to model a force that acts on a particle during an interval of time.
* Students will learn how to model a force that acts on a particle based on the position of the object.

## Forces That Act _Conditionally_

So far when we have written code to define a force in Tychos we have created those forces to act on particles the entire duration of the simulation. This works fine if you are trying to simulate gravity acting on an object on Earth for example because the force of gravity is always acting upon that object.

But as you know, not all forces work like this. For example, you might only be pushing on a ball for a certain amount of time, so you want the force to disappear once the ball has left your hand.

In these cases, we want to model a force that acts on an object only when a certain condition is met. Let's look at an example. Below is a simulation of a particle \(represented by a rocket!\) that is being accelerated by a force that exists for the entire duration of the simulation. In this case it is a force that only points in the positive horizontal direction.

The code for that force is as you would expect:

```text
F1 = [10, 0]
```

And we then define a net force, which right now only includes this one force:

```text
Fnet = F1
```

But lets say we want to have the force _F1_ only act on it during a certain time interval - this is where we must use something called a conditional operation.

### Conditional Statement

In Tychos we can use a conditional statement which evaluates an expression to either _true_ or _false_. Here is an example of a conditional statement:

```text
(t > 2)
```

This is a very simple statement that Tychos will evaluate every frame of the simulation. Put this line of code into the **Calculations** pane in Tychos and you should see the output text go from this:

![](https://tychos.org/static/lessons/lesson_cf1.png)

to this:

![](https://tychos.org/static/lessons/lesson_cf2.png)

Before the simualtion time reaches 2 seconds, Tychos evaluates the statement as _true_. Once the time in the simulation has passed 2 seconds, Tychos evaluates the conditional statement and prints the output as _false_.

### Comparison Operators

Conditional statements use comparison operators to compare values of two things. You have seen some of the comparison operators before, but some you might not be familar with. Here is a list of some of the comparison operators and how they work:

| Operator | Example | Evaluates | Description |
| :--- | :--- | :--- | :--- |
| &lt; | 1 &lt; 2 | true | Less than |
| &gt; | 1 &gt; 2 | false | Greater than |
| &lt;= | 1 &lt;= 2 | true | Less than or equal |
| &gt;= | 1 &gt;= 2 | false | Greater than or equal |
| != | 1 != 2 | true | Not equal |
| == | 1 == 2 | fasle | Equal |
| deepEqual | deepEqual\(\[0, 0\], \[0, 1\]\) | false | Equality of matrices |

The last one is actually a function, not a comparison operator and it is used to check if two matrices elements are both equivalent.

### Setting A Conditional Value 

In Tychos, and many other computer languages, the value _true_ can be represented as the number 1, and the value of _false_ is also represented as 0. Let's demonstrate to make this more obvious.

Change the line of code that you just wrote with this:

```text
5 * (t < 2)
```

What you should see now is that instead of printing out _true_ before the 2 seconds have elapsed, you should see the digit _5_, but then when the time is greater than 2 seconds, the value printed to the screen is _0_. What we have done here is used the fact that when _t_ is less than 2, the statement is evaluated as true which is mathematically equivalent to 1. Once _t_ is larger than 2, the conditional statement is evaluated as false which is mathematically equivalent to 0.

Multiplying a force with a conditional statement can allow us to "turn on" or "turn off" a force based on a condition - in this case the condition that time is less than 2 seconds. Change the line of code for _F1_ so that it now looks like this:

```text
F1 = [10, 0] * (t < 2)
```

Now play the simulation and you should see that the particle accelerates for 2 seconds, and then after that, it moves at a constant velocity. Look at the graph to verify that this is how it behaves. You should see a graph for the X position thta shows a curve at the beginning but then it becomes a straight line with an unchanging slope:

![](https://tychos.org/static/lessons/lesson_cf3.png)

We now have a way to model a force acting on an object such that it stops after a specified amount of time.

### Logical Operators

In the example above the force exists until two seconds into the simulation and then it becomes zero forever afterward. What if we wanted a force to exist between two times?

We can actually set a condition for an interval by using what is known as a **logical operator**. A logical operator allows you to combine conditions. So for example you might want the force to act on the particle after 3 seconds AND before 5 seconds. This is done by using the keyword _and_.

Let's define a second force that will exist during this interval:

```text
F2 = [-10, 10] * ((t > 3) and (t < 5))
```

Notice that we added another conditional statement _\(t &lt; 5\)_ after the logical operator _and_. It is important that you use another set of parentheses around both conditional statements. We now need to change the net force calculation:

```text
Fnet = F1 + F2
```

When you start the simulation, you should see that after three seconds, a different force is applied on the particle and then it disappears after 5 seconds.

Another logical operator that can be used is the logical _or_. This can be used to define two different conditions that are exclusive. For example we could say that the force exists on the particle before 2 seconds OR after 5 seconds. Let's change the code that defines _F1_:

```text
F1 = [10, 0] * ((t < 2) or (t > 5))
```

Now when you run the simulation, you can see that the particle is once again acted on by _F1_ after 5 seconds.

You can even combine logical operators as long as you use parentheses like this:

```text
F1 = [10, 0] * ((t < 2) or ((t > 5) and (t < 7)))
```

Now when you run the simulation, you should see that _F1_ now acts on the particle from 0 to 2 seconds, and then again between 5 seconds and 7 seconds.

## Turning The Rocket!

There is a way to get the rocket to turn in the direction that it is headed. There is a function that can be used called `rotate`. If we want the rocket to turn a certain number of degrees, we simply write:

```text
rocket.rotate(-90)
```

If want it to turn the direction of its own velocity, we use a different function called `direction` which returns the direction in degrees for a vector. Combining the two like this:

```text
rocket.rotate(direction(rocket.v) - 90)
```

For this example, I had to turn the rocket by -90 degrees, so you will have to do that as well.

### Other Conditions

You can use a conditional in many ways. So far we have seen how you could use it to control _when_ a force is being applied, but you could also use it to define _where_ a force is applied. For example, what if we wanted to simulate a ball moving across a table, but once it reached the end of the table, it behaved like a projectile.

Look at the simulation below:

When you play the simulation, the ball continues to travel in a straight path off our virtual table, and floats! In this simulation, the normal force continues to act on the ball after it has left the table. What we really want to do is make the normal force disappear once the ball reaches the end of the table. We can easily fix this with a conditional. Notice that the table edge is located at X = 50.  Open the **Calculations** pane and change this line of code:

```text
Fn = -Fg
```

To this:

```text
Fn = -Fg * (ball.pos[X] < 50)
```

When you play the simulation, you should see that when the ball reaches the edge of the table, it begins to move like a projectile!

This demonstrates that we can control the forces acting on a particle by conditionally changing the force based on a time interval or where the object is. This is going to be very helpful as we learn to make more and more realistic and complex simulations.

### Rotating The Ball!

There is a way to get the rotate. You can use the `rotate` function again. Its a bit tricker because the rate at which the ball would rotate depends on the speed of the ball, and the direction that it is traveling. In a future tutorial we will look at rotational dynamics, but for now I will give you a hint.

The ball has an attribute called  that stores the current angle of rotation that the image is rotated. This is just a variable, like any other that can be updated. Try this line of code in the **Calculations** pane:

```text
ball.rotate(ball.angle - 10)
```

If you really want the ball to rotate realistically, you would need to somehow get the rate of rotation to be dependent on the rate of the ball's speed...

## Conclusion

This was a brief but important tutorial on how to simulate forces that exist conditionally. The actual programming concept is what is known as a conditional statement, and we will learn that we can use conditional statements to modify the behavior of other things.

Here are the basic steps of defining a conditional force:

1. Define a force using a matrix, just like we have done before.

   ```text
   F1 = [10 , 0]
   ```

2. Multiply the force with conditional statement using one of the **comparison operators** above \(&lt;, &gt;, !=, ==, etc.\)

   ```text
   F1 = [10, 0] * (t > 3)
   ```

3. Use a logical operator to define multiple conditions:  


   ```text
   F1 = [10, 0] * ((t > 3) and (t < 5))
   ```

4. Define a net force that is just the sum of all fores acting on the object. This way you can combine more than one conditional force.

   ```text
   Fnet = F1 + F2
   ```

5. Use the same method that we have used \(the Momentum Principle!\) to update the particle's velocity, and then its position.

