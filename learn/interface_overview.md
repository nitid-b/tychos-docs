___
[TOC]
___
# Interface Overview
The following page describes the primary interface elements of the Tychos application. 

---

### World View
The main application screen shows the simulated world filled with particles, and any graphs that have been defined. The main window primarily consists of a two dimensional grid that represents a limitless two dimensional euclidean space. This is the space where all simulation animations take place.
<div class="panel panel-default">
<div class="panel-body"><p class="text-center img-rounded"><img src="/static/help/ui/ui_world_view.png" style="width: 700px;" /></p></div>
</div>
There are several key user interface elements on the screen that serve important functions for accessing different aspects of the application:
<ol>
  <li>Wrench Icon - click on this to access the editing and settings panel for your simulations.</li>
  <li>Links Menu - click on this to access links to other content on our website.</li>
  <li>Simulation Controls - these are the controls for starting, stepping through, stopping or saviing your simulation.</li>
</ol> 
---
### Simulation Editing Panels
The panels shown below are accessed by clicking the small wrench icon in the upper left hand corner of the screen. Each panel has its own function with different information displayed and often editable by the user.
<div class="container">
<hr />
<section markdown="1">
#### Description Panel
</section>
<div class="row">
  <div class="col-md-6">This is the description of the simulation, as well as any optional directions that can be identifed by the simulation author.</div>
  <div class="col-md-6"><img src="/static/help/ui/ui_desc_panel.png" class="image-right img-rounded" style="width: 400px;" /></div>
</div>
<hr />
<section markdown="1">
#### Goals Panel
</section>
<div class="row">
  <div class="col-md-6">The instructor or whoever wrote the scenario may include specific goals that the student should accomplish with this Scenario.  Each goal has a description such as "Make particle p1 move to the right" and the goal will turn green when your program achieves that goal.</div>
  <div class="col-md-6"><img src="/static/help/ui/ui_goal_panel.png" class="image-right img-rounded" style="width: 400px;" /></div>
</div>
<hr />
<section markdown="1">
#### Initial State Panel
</section>
<div class="row">
  <div class="col-md-6">You program the initial conditions of the simulation, e.g. creating particles, setting their initial position, creating graphs to view particular aspects of your simulation, and perhaps defining initial values such as the gravity or mass. The code that you write appears on the left of the screen, while each line of code is evaluated and its output appears on the right in blue text. You can learn more about what kind of code can be written in this pane by visiting the <a href="/doc/learn/reference.html">Language Reference</a></div>
  <div class="col-md-6"><img src="/static/help/ui/ui_is_panel.png" class="image-right img-rounded" style="width: 400px;" /></div>
</div>
<hr />
<section markdown="1">
#### Calculations Panel
</section>
<div class="row">
  <div class="col-md-6">In this panel, you write your program for calculating what the simulation does for every moment in time as the simulation runs - called a frame. E.g. for a simulation of particles moving in space, you might examine several particles and calculate a new position for them given their existing momentum. Just as in the <strong>Initial State</strong> pane, the code that you write appears on the left of the screen, while each line of code is evaluated and its output appears on the right in blue text. You can learn more about what kind of code can be written in this pane by visiting the <a href="/doc/learn/reference.html">Language Reference</a></div>
  <div class="col-md-6"><img src="/static/help/ui/ui_calc_panel.png" class="image-right img-rounded" style="width: 400px;" /></div>
</div>
<hr />
<section markdown="1">
#### Settings Panel
</section>
<div class="row">
  <div class="col-md-6">This pane allows you to change several settings of the simulation:
  <ul>
  <li>A button for displaying or hiding a <strong>Motion Map</strong></li>
  <li>A slider for adjusting the frame rate.</li>
  <li>A slider for adjusting the motion map's strobe rate.</li>
  <li>An input box for setting the amount of time the simulation runs. A value of -1 tells the simulation to run indefinitely.</li>
  <li>There are several settings for adjusting how the World View is displayed. The World View window can either scale automatically depending on the space inhabited by any particles, or it can be set to a specific viewing size.</li>
  </ul>
  </div>
  <div class="col-md-6"><img src="/static/help/ui/ui_settings_panel.png" class="image-right img-rounded" style="width: 400px;" /></div>
</div>
</div>
