# Recommended Components and Nodes

Unity has a lot of different components and scripting nodes available. Finding the ones you need can prove very difficult, especially since there is very little documentation. 
The official [Node reference](https://docs.unity3d.com/Packages/com.unity.visualscripting@1.7/manual/vs-nodes-reference.html) page lists a handful of important nodes, 
but there are more we will be using (and many more than that besides). This page is intended as a reference to the subset of important nodes you will need for COMP1151.
The list is broken down by component.

Some of these nodes as labelled as 'Custom'. These have been written by the teaching staff as extensions to Unity to provide useful features. These will be included in
your prac or assignment framework code for you to use. You are also welcome to use these in your own projects, without restriction.

## Contents

* [Event Nodes](#event-nodes)
* [Variable Nodes](#variable-nodes)
* [Control Nodes](#control-nodes)
* [Formula Nodes](#formula-nodes)
* [Transform](#transform)
* [Time](#time)
* [Vector2](#vector2)
* [Input (Custom)](#input-custom)

---
## Event Nodes
You can think of lifecycle events as starting points within your scripts. They will each trigger under different conditions and execute all connected nodes.

### On Start ##
This event triggers exactly once when the script is first enabled, before the On Update event. Usually, this will occur as soon as you start your game, but it can also trigger if you enable an object for the first time (using something like Set Active). Note this can only occur once, so if you disable the object and re-enable it again, it won’t trigger again.

Inputs: 
None

Outputs: 
Trigger (Flow): The next node to execute.

Use Case Examples: 
- Setting variables


### On Update ##
This event triggers once every frame while the script is enabled. This is useful for any continuous or repeating things and will likely be the lifecycle event you use the most.

Inputs: 
None

Outputs: 
Trigger (Flow): The next node to execute.

Use Case Examples:
- 


### Trigger Events ##
These events will occur whenever a collision between this object and another is detected. In this case, a collision can be defined as two colliders overlapping. There must be at least one trigger collider and one Rigidbody 2D involved. It doesn’t matter which object these components are attached to.

Depending on the types of colliders involved, a trigger event may not occur. Most notably with trigger colliders, two static trigger colliders (meaning they are not using Rigidbodies) cannot interact with one another.

https://docs.unity3d.com/2017.4/Documentation/Manual/CollidersOverview.html 

On Enter 2D
This event occurs once each time a collision is detected. It can be triggered again with the same object if the colliders stop touching and collide again.

Inputs: 
Target (GameObject): If a GameObject is passed into this, the node will only execute when a collision with the specified GameObject is detected.

Outputs: 
Trigger (Flow): The next node to execute.
Collider (Collider 2D): The collider component of the colliding object.

Use Case Examples:
- 

On Exit 2D
This event occurs once after two colliders stop colliding (in that they stop touching). It can be triggered again with the same object if the objects collide again and stop touching.

Inputs: 
Target (GameObject): If a GameObject is passed into this, the node will only execute when a collision with the specified GameObject is detected.

Outputs: 
Trigger (Flow): The next node to execute.
Collider (Collider 2D): The collider component of the colliding object.

Use Case Examples:
- 
On Stay 2D
This event occurs every physics timestep (by default, 50 times per second) while two colliders are touching.

https://docs.unity3d.com/6000.0/Documentation/Manual/fixed-updates.html 

The script may stop detecting collisions if the object stops moving. This is because the rigidbody thinks it’s at rest and is put to sleep. To disable this, go to the object’s Rigidbody 2D component and set its Sleeping Mode to Never Sleep.

<image>

https://docs.unity3d.com/6000.0/Documentation/ScriptReference/Rigidbody2D-sleepMode.html 

Inputs: 
Target (GameObject): If a GameObject is passed into this, the node will only execute when a collision with the specified GameObject is detected.

Outputs: 
Trigger (Flow): The next node to execute.
Collider (Collider 2D): The collider component of the colliding object.

Use Case Examples:
- 


### Collision Events ##
These events will occur whenever a physical collision occurs between two non-trigger colliders. In this case, a collision can be defined as two colliders overlapping. One of the colliders must also be a dynamic collider, meaning it has a Rigidbody 2D component that is set to Dynamic mode.
<image>

The outputs of these nodes are quite extensive, containing all sorts of information about the collision that occurred. This is generally most useful for responding dynamically to collisions.
On Enter 2D
This event occurs once each time a collision is detected. It can be triggered again with the same object if the colliders stop touching and collide again.

Inputs: 
Target (GameObject): If a GameObject is passed into this, the node will only execute when a collision with the specified GameObject is detected.

Outputs: 
Trigger (Flow): The next node to execute.
Collider (Collider 2D): The collider component of the colliding object.
Contacts (Contact Point 2D Array): An array of ContactPoint2Ds. These objects contain quite a bit of information, but most notably, they can tell you exactly where the collision occurred in world coordinates. (https://docs.unity3d.com/6000.0/Documentation/ScriptReference/ContactPoint2D.html )
Relative Velocity (Vector 2): The velocity of the collision. You can treat it like the force and direction of the collision.
Enabled (Boolean): Whether a collision response is enabled or not.
Data (Collision 2D): Contains all of the above information, plus a lot extra (https://docs.unity3d.com/6000.0/Documentation/ScriptReference/Collision2D.html )

Use Case Examples:
- Creating particle effects when two objects collide.
On Exit 2D
This event occurs once after two colliders stop colliding (in that they stop touching). It can be triggered again with the same object if the objects collide again and stop touching.

Inputs: 
Target (GameObject): If a GameObject is passed into this, the node will only execute when a collision with the specified GameObject is detected.

Outputs: 
Trigger (Flow): The next node to execute.
Collider (Collider 2D): The collider component of the colliding object.
Contacts (Contact Point 2D Array): An array of ContactPoint2Ds. These objects contain quite a bit of information, but most notably, they can tell you exactly where the collision occurred in world coordinates. (https://docs.unity3d.com/6000.0/Documentation/ScriptReference/ContactPoint2D.html )
Relative Velocity (Vector 2): The velocity of the collision. You can treat it like the force and direction of the collision.
Enabled (Boolean): Whether a collision response is enabled or not.
Data (Collision 2D): Contains all of the above information, plus a lot extra (https://docs.unity3d.com/6000.0/Documentation/ScriptReference/Collision2D.html )

Use Case Examples:
On Stay 2D
This event occurs every physics timestep (by default, 50 times per second) while two colliders are touching.

Inputs: 
Target (GameObject): If a GameObject is passed into this, the node will only execute when a collision with the specified GameObject is detected.

Outputs: 
Trigger (Flow): The next node to execute.
Collider (Collider 2D): The collider component of the colliding object.
Contacts (Contact Point 2D Array): An array of ContactPoint2Ds. These objects contain quite a bit of information, but most notably, they can tell you exactly where the collision occurred in world coordinates. (https://docs.unity3d.com/6000.0/Documentation/ScriptReference/ContactPoint2D.html )
Relative Velocity (Vector 2): The velocity of the collision. You can treat it like the force and direction of the collision.
Enabled (Boolean): Whether a collision response is enabled or not.
Data (Collision 2D): Contains all of the above information, plus a lot extra (https://docs.unity3d.com/6000.0/Documentation/ScriptReference/Collision2D.html )

Use Case Examples:

---
## Variable Nodes
Variables are a way to store/contain information in a script. They are a fundamental part of your scripts (and all of programming in general). Each variable has a type and a value. The type specifies the kind of data it can contain and the value is the data it does contain. There are also a number of scopes for you to use with your scripts. These determine where a variable can be accessed from.

Variables can be created and managed via the blackboard in the Script Graph window.
<Image>

Common Types:
Float: A number with decimal places. Can be positive or negative.
Integer: A whole number. Can be positive or negative.
String: Text data.
Vector 2: A pair of floats. Intended to represent x and y values (for movement or positions).
Game Object: Any GameObject.

Scopes: 
Flow: Variables created within a graph. They cannot be created through the blackboard and only exist within the logical flow where they were created. To give an example, if you created a flow variable in the On Update event, it would only be accessible in that On Update event after it was created. You likely won’t need to use these.
Graph: Variables are only accessible within the graph they are associated with. They cannot be accessed by other graphs on the same object.
Object: Variables are only accessible within the GameObject. If an object has multiple graphs, they will all be able to access these variables.
Scene: Variables are accessible by all graphs within the same scene.
App: Variables accessible throughout the entire game.
Saved: These variables are also accessible throughout the entire scene. They persist, even after the game is closed. This can be used to create a basic save system.

https://docs.unity3d.com/Packages/com.unity.visualscripting@1.7/manual/vs-variables.html 

Links: 

### Get Variable
This node is used to read the value of a variable. At the top, there is a dropdown menu that allows you to select the scope you would like to get the variable from.

<Image>

Inputs: 
Name (String): The name of the variable to access.

Outputs: 
Value (Object): The value of the variable being accessed.

Use Case Examples:
- 

### Set Variable
This node is used to change the value of a variable. At the top, there is a dropdown menu that allows you to select the scope you would like to get the variable from.

<Image>

Inputs: 
Assign (Flow): The node to execute before this one.
Name (String): The name of the variable to access.
New Value (Object): The value to change the variable to. Make sure the value is the correct type.

Outputs: 
Assigned (Flow): The next node to execute.
Value (Object): The value of the variable after setting it.

Use Case Examples:
- 

---
## Control Nodes

General information about control nodes can be found in the [Unity documentation](https://docs.unity3d.com/Packages/com.unity.visualscripting@1.7/manual/vs-control.html). 
The main control nodes we will be using are listed below.

These nodes allow you to change the control flow of your scripts, allowing them to branch off and converge to do different things based on various conditions. Without them, your scripts would probably be a lot less responsive.

### If node
This node allows you to change the control flow based on a condition. Basically, that means you can create branching paths in your scripts. You can generally read an if statement as: “If the given condition is true, do something, otherwise, do something else.”

You do not necessarily need to assign both output pipes to any other nodes. If you don’t, the control flow will end if the script tries to go down the unassigned true/false path.

Inputs: 
Enter (Flow): The node to execute before this one.
Condition (Boolean): The condition used to choose between the two paths.

Outputs: 
True (Flow): The next node to execute if the condition is true.
False (Flow): The next node to execute if the condition is false.

Use Case Examples:

### Select node
This node outputs one of two values based on a condition. If the condition is true, it will output the first value passed in, if it’s false, it will output the other.

Both value inputs must be assigned some value, otherwise, this node will not work.

Inputs: 
Condition (Boolean): The condition used to choose the output.
True (Object): The value to output if the condition is true.
False (Object): The value to output if the condition is false.

Outputs: 
Selection (Object): The value to output.

Use Case Examples:

### For loop
This node allows you to repeat a certain section of your graph a specified number of times. Anything attached to the body output will be repeated.

The way it works is that you provide it with a first value, last value and step value. It also separately keeps track of an index value (this can be accessed from the index output). The loop will then execute these steps:
1. Set the index value equal to the first value.
2. Check if the index is less than the last value.
   a. If it is less, continue to step 3.
   b. If it is greater than or equal to, the loop ends and the script executes the exit output.
3. The body output is executed once.
4. Add the step value to the index.
5. Repeat from step 2.

Inputs: 
Enter (Flow): The node to execute before this one.
First (Integer): The starting value for the index.
Last (Integer): The ending value for the index.
Step (Integer): The amount to add to the index in each loop iteration.

Outputs: 
Exit (Flow): The node to execute after the loop completes.
Body (Flow): The node to execute each time the loop repeats.
Index (Integer): The current index of the loop.

Use Case Examples:
- Spawning multiple prefabs at once. For example, if you wanted to spawn ten enemies simultaneously, it would be quite inefficient to create ten instantiate nodes, so instead, you can create a for loop that repeats the instantiate node ten times.

---
## Formula Nodes

General information about formula nodes can be found in the [Unity documentation](https://docs.unity3d.com/Packages/com.unity.visualscripting@1.7/manual/vs-formula.html). 
The main control nodes we will be using are listed below.

These allow you to perform arithmetic within your graphs. There is a very large range of math nodes available to you, so it’s worth looking into, especially if you want to do things like custom physics.

Note that there are multiple variants of these nodes. We will generally be using the Math/Generic versions, which allows the use of any applicable data types (not just numbers). This means we can do things like concatenating strings or performing arithmetic with vectors.

Links: 


### Add Node
Allows you to add values together. Note that this node allows you to control the number of inputs to add together (up to 10) using the input field near the top of the node. None of the other Math/Generic nodes let you do this.

<image>

Inputs: 
A (Object): The first value to add.
B (Object): The second value to add.
C… J (Object): All other values to add.

Outputs: 
Sum (Object): The result of the addition.

### Subtract Node
Allows you to subtract one value from another.

Inputs: 
A (Object): The value to subtract from.
B (Object): The value to subtract.

Outputs: 
A - B (Object): The result of the subtraction.

### Multiply Node
Allows you to multiply two values.

Inputs: 
A (Object): The first value to multiply.
B (Object): The second value to multiply.

Outputs: 
A x B (Object): The result of the multiplication.

### Divide Node
Allows you to divide one value by another.

Inputs: 
A (Object): The value to divide.
B (Object): The value to divide by.

Outputs: 
A ÷ B (Object): The result of the division.

### Modulo Node
Allows you to perform modulo arithmetic. It divides the first term by the second and outputs the remainder. It’s useful for looping counters or screen wrapping.

Inputs: 
A (Object): The value to divide.
B (Object): The value to divide by.

Outputs: 
A % B (Object): The remainder after dividing.

---
## Transform
This component is responsible for the position, rotation and scale of your GameObjects. All GameObjects should have one automatically if they exist within a scene. It has quite a few nodes and functions for manipulating these three aspects of your objects.

### Get Position/Rotation/Scale (Local / Global)

### Set Position/Rotation/Scale (Local / Global)

### Translate

### Rotate

---
## Time
The time class allows you to interact with many different aspects of time within your games, like seeing how long your levels have been loaded for or checking framerate information. We won’t be using too much of that outside of delta time, but it’s worth being aware of its existence.

### Get Delta Time
Allows you to check the time interval between frames. Frame rate can be variable (as you may have experienced if you have a not-so-up-to-date PC and are trying to play an intensive game), so making things dependent on it can lead to unexpected behaviours at different frame rates, like the same characters/objects moving at different speeds or certain inputs and actions becoming impossible. Applying delta time to any frame rate-based actions (e.g. translating an object in the update event) will instead make them time-based and thus remove any frame rate discrepancies.

Inputs: 
None

Outputs: 
Float: Seconds since last frame.

Use Case Examples: 

---
## Vector2

### Magnitude

### Normalize

### Rotate (Custom)

### IsOnLeft (Custom)

---
## Debug

### Log

---
## Input (Custom)

### Get Input Button

### Get Input Axis

### Get Input Vector2

