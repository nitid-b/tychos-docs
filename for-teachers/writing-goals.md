# Writing Goals

## Overview <a id="writing-goals"></a>

A _goal_ in Tychos is a short piece of code in a _scenario_ which can check a student's work. Goals are written by the scenario's author, usually an instructor. To the student, the goals appear as a sentence describing something the student should do. The goal will start out black when the student clicks Run. At a time defined within the goal, the goal is "checked" and if the goal is satisfied, it turns green. Otherwise it turns red.

See an example:

{% embed url="https://tychos.org/scenarios/31" caption="https://tychos.org/scenarios/31" %}

A goal has three parts: \(1\) a **description** which the student sees, \(2\) a **when condition** which specifies at what time the goal will be checked, and \(3\) the **victory condition** which specifies what value the student is supposed to create. Here is a simple goal:

Goal 1 - _description:_ Create a variable 'b' and set it to 3. - _when:_ `t == 0` - _victory:_ `b == 3`

The above goal's _when condition_, when `t` is 0, causes the victory condition will be checked right after the _initial state_ code is run, and before the first _calculations_ code is run. To satisfy this goal, the student can write this:

```text
# Intial State
b = 3
```

Note that if the student writes `b=3` in the _calculations_ editor, the goal will not be satisfied because no calculations are run yet at `t==0`

Here is another goal that will check that a student can increment a value in the calculations editor:

Goal 2 - _description:_ Increment 'b' by 2 every frame - _when:_ `frame_count == 10` - _victory:_ `b == 23`

With these two goals, you are checking that the student has properly set the initial condition, and that every frame, `b`'s value is incrementing by two.

## Writing a Goal

In order to write a goal, you need to be logged in as an Instructor. Only instructors see blue edit buttons over the goals. See illustration.

![](http://localhost:3000/static/writing_goals/goal-4.png)When you click the pencil button to edit a goal, the goal turns into three edit boxes that contain the **description**, **when** the goal should be checked, and the **victory condition**. The description is for the student to read and must be specific enough for the student to understand what to do. The two conditions are bits of code that specify:

* _when condition:_ When the victory condition should be run, e.g. at t=0 or when a particle's X position = 10.
* _victory condtiion:_ What would indicate the student has accomplished the goal.

### Writing the Description <a id="writing-the-description"></a>

Descriptions are just English sentences that tell the student what your goal is going to check for. Descriptions are similar to quiz questions—they are easy to misinterpret. It's useful to have someone proof-read your descriptions to see if there are other interpretations of what you have written.

### Writing the When condition <a id="writing-the-when-condition"></a>

The When condition is needed to tell the goal when it should check the student's work. For example if you want the student to create a variable named `b` and assign it the value `3`, then you would might have the goal check at `frame_count == 0` which means right at the beginning.

But if you want to see if the student is changing a variable in the _calculations_ editor, then you'll want to check in later frames since the frame 0 is just the _initial state_ editor and later frames run the code in _calculations_.

Another variable you might check is `t` which is how many seconds have elapsed in the simulation.

### Example: Writing a Victory condition on a particle's X position <a id="writing-a-victory-condition-on-a-particles-x-position"></a>

The Victory condition code will be checked when the _when condition_ is satisfied. Generally the victory condtion code will check a variable which you have asked the student to set. It might be set directly such as "create a variabe `b` and set it to `3`", or might be indirect. For example if you want a student to write:

```text
# Initial State
v = [5, 0]
p = Particle([0,0])

# Calculations:
p.pos = p.pos + v * dt
```

Then here is a goal that checks the proper p.pos at 1 second:

Goal 3 - _description:_ Make a particle `p` start at X=0 and move to the right 5 units per second. - _when condition:_ `t == 1` - _victory condition:_`p.pos[X]==5`

#### Checking matrix values <a id="checking-matrix-values"></a>

Goal 3 checked only the X position of the particle. If you want to check both X and Y, or if you have a bigger matrix, you don't want to check each element individually. You might think comparing two matrices is what you want, e.g. `p.pos == [10,20]`. Try typing this into the calculations editor to see what happens: it returns `[true, true]` — it's comparing each element of those two matrices. That won't work for a goal.

Instead you need the MathNotepad function [`deepEqual`](http://mathnotepad.com/docs/functions.html#function=deepEqual) like so: `deepEqual(p.pos, [10, 20])` which returns either `true` or `false`.

Goal 4 - _description:_ Create a force vector 'f' and set it to a horizontal value of 0, and a vertical value of 50. - _when condition:_ `t == 0` - _victory condition:_ `deepEqual(v, [0, 50])`

#### Checking distance between two positions <a id="checking-distance-between-two-positions"></a>

For a goal to check the distance between two points, use the MathNotepad function [`distance`](http://mathnotepad.com/docs/functions.html#function=distance)

Goal 5 - _description:_ Adjust when the force 'f' starts so that particle 'p' moves within 25 meters of the goal \[50, 500\] at 10 seconds. - _when condition:_ `t == 10` - _victory condition:_ `distance(p.pos, [50, 500]) < 25`

