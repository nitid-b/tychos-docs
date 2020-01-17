# Change Log

## 2020-1-03

### Fixed

* Some scenarios were crashing when the Settings pane was opened. We found the problem and now all scenarios should have an accessible Settings pane.

## 2019-8-19

### Added

* **Data Output Table:** This is has been a feature that we have wanted to add for quite some time, and we have an initial version ready for you! With just a few lines of code, you can now create a data table for displaying variable values. This can be really helpful for recording a history of the simulation. We think this is a crucial tool for helping students connect the code they write to the simulation animation. You can create a data table by setting the columns in the Initial State Pane like this:  `table.setColumns(["column1", "column2", ...])`  Where the array of strings `"column1"` and `"column2"` would be the table column headers. You must have a table with at least one column, but you can have many more. Then you can record a new row in the table using this command in the Calculations Pane:  `table.addRow([val1, val2, ...])`  Where the array of values for example - `val1` and `val2` - could be any variable values you would like to record. The array of values must have the same number of values as columns in the table. 
* **Mouse Interactivity** You can now get the position of the mouse mapped to the simulation extents. This allows you, for example, to build interactive simulations where Particles or Blocks can respond to the mouse position. To do so, you simply just need to reference the mouse position like this:  `mouse.pos`  This will return the mouse position within the scenario coordinate system. We have also added the ability to detect “mouse over” events. The following function allows you to test if the mouse is over a Particle or a Block:  `# Where p is a Particle, but could be a Block too! mouse.is_over(p)`  Here is a demonstration to check out these the new mouse interaction features:  [https://tychos.org/scenarios/nQqTE7](https://tychos.org/scenarios/nQqTE7) 





