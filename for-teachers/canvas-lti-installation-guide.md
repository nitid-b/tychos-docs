# Canvas LTI Installation Guide

## Tychos Works with Instructure Canvas <a id="tychos-works-with-instructure-canvas"></a>

### What's good about Canvas LTI Apps? <a id="whats-good-about-canvas-lti-apps"></a>

When using LTI, Canvas will tell Tychos who is logged in. This allows your students to save copies of your master scenario under their name. If the same student clicks the module again in Canvas, they will get their last saved version of the Scenario instead of the master scenario.

### Adding Tychos as a Canvas LTI App <a id="adding-tychos-as-a-canvas-lti-app"></a>

This app can be installed as an LTI plugin with Instructure Canvas. Here is how to do it

* In Canvas, go to Settings &gt; Apps &gt; View App Configurations
* Click the blue "+" button. You should see the Add App form. Fill it out like so:

![](https://tychos.org/static/lti_help/Tychos-Canvas-external-apps-edit.png)

### Adding a Tychos Scenario as a Canvas Module <a id="adding-a-tychos-scenario-as-a-canvas-module"></a>

* Go to the Scenario you want to add. Take a note of the number in your URL. E.g. tychos.org/scenarios/13 means your scenario is number **13**.
* In Canvas, go to Modules &gt; "+" Button. You should see the Add Item to... popup. Choose:
* Add: **External Tool**
* Click on **Tychos**. Notice the URL gets filled in with a URL ending with `...tychos.org/lti`
* **URL**: Add your scenario number from above to the end of the URL, e.g. `...tychos.org/lti/13`
* **Page Name**: copy the name of your Scenario
* Click Add Item

