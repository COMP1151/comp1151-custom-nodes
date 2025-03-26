![image](https://github.com/user-attachments/assets/117be40c-4a6c-4ceb-bbec-3fb97f31719e)# Recommended Components and Nodes

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

Read more about events [here](https://docs.unity3d.com/Packages/com.unity.visualscripting@1.7/manual/vs-events-reference.html).

### On Start ##
This event triggers exactly once when the script is first enabled, before the On Update event. Usually, this will occur as soon as you start your game, but it can also trigger if you enable an object for the first time (using something like Set Active). Note this can only occur once, so if you disable the object and re-enable it again, it won’t trigger again.

<img src="Images\Start Node.png">

Inputs: 
- None

Outputs: 
- Trigger (Flow): The next node to execute.

### On Update ##
This event triggers once every frame while the script is enabled. This is useful for any continuous or repeating things and will likely be the lifecycle event you use the most.

<img src="Images\Update Node.png">

Inputs: 
- None

Outputs: 
- Trigger (Flow): The next node to execute.

---
## Trigger Events
These events will occur whenever a collision between this object and another is detected. In this case, a collision can be defined as two colliders overlapping. There must be at least one trigger collider and one Rigidbody 2D involved. It doesn’t matter which object these components are attached to.

Depending on the types of colliders involved, a trigger event may not occur. Most notably with trigger colliders, two static trigger colliders (meaning they are not using Rigidbodies) cannot interact with one another.

Please note that there are 2D and 3D variants of these nodes. Make sure you are using the 2D ones.

Read more about collision [here](https://docs.unity3d.com/6000.0/Documentation/Manual/collision-section.html).

### On Enter 2D ##
This event occurs once each time a collision is detected. It can be triggered again with the same object if the colliders stop touching and collide again.

<img src="Images\On Trigger Enter 2D Node.png">

Inputs: 
- Target (GameObject): If a GameObject is passed into this, the node will only execute when a collision with the specified GameObject is detected.

Outputs: 
- Trigger (Flow): The next node to execute.
- Collider (Collider 2D): The collider component of the colliding object.

### On Exit 2D ##
This event occurs once after two colliders stop colliding (in that they stop touching). It can be triggered again with the same object if the objects collide again and stop touching.

<img src="Images\On Trigger Exit 2D Node.png">

Inputs: 
- Target (GameObject): If a GameObject is passed into this, the node will only execute when a collision with the specified GameObject is detected.

Outputs: 
- Trigger (Flow): The next node to execute.
- Collider (Collider 2D): The collider component of the colliding object.

### On Stay 2D ##
This event occurs every physics timestep (by default, 50 times per second) while two colliders are touching. More info [here](https://docs.unity3d.com/6000.0/Documentation/Manual/fixed-updates.html).

<img src="Images\On Trigger Stay 2D Node.png">

The script may stop detecting collisions if the object stops moving. This is because the rigidbody thinks it’s at rest and is put to [sleep](https://docs.unity3d.com/6000.0/Documentation/ScriptReference/Rigidbody2D-sleepMode.html). To disable this, go to the object’s Rigidbody 2D component and set its Sleeping Mode to Never Sleep.

<img src="Images\Never Sleep.png">

Inputs: 
- Target (GameObject): If a GameObject is passed into this, the node will only execute when a collision with the specified GameObject is detected.

Outputs: 
- Trigger (Flow): The next node to execute.
- Collider (Collider 2D): The collider component of the colliding object.

---
## Collision Events
These events will occur whenever a physical collision occurs between two non-trigger colliders. In this case, a collision can be defined as two colliders overlapping. One of the colliders must also be a dynamic collider, meaning it has a Rigidbody 2D component that is set to Dynamic mode.

The outputs of these nodes are quite extensive, containing all sorts of information about the collision that occurred. This is generally most useful for responding dynamically to collisions.

Please note that there are 2D and 3D variants of these nodes. Make sure you are using the 2D ones.

Read more about collisions [here](https://docs.unity3d.com/6000.0/Documentation/Manual/collision-section.html).

### On Enter 2D ##
This event occurs once each time a collision is detected. It can be triggered again with the same object if the colliders stop touching and collide again.

<img src="Images\On Collision Enter 2D Node.png">

Inputs: 
- Target (GameObject): If a GameObject is passed into this, the node will only execute when a collision with the specified GameObject is detected.

Outputs: 
- Trigger (Flow): The next node to execute.
- Collider (Collider 2D): The collider component of the colliding object.
- Contacts (Contact Point 2D Array): An array of [ContactPoint2D](https://docs.unity3d.com/6000.0/Documentation/ScriptReference/ContactPoint2D.html)s. These objects contain quite a bit of information, but most notably, they can tell you exactly where the collision occurred in world coordinates.
- Relative Velocity (Vector 2): The velocity of the collision. You can treat it like the force and direction of the collision.
- Enabled (Boolean): Whether a collision response is enabled or not.
- Data (Collision 2D): Contains all of the above information, plus a lot extra. All of it can be found [here](https://docs.unity3d.com/6000.0/Documentation/ScriptReference/Collision2D.html).

### On Exit 2D ##
This event occurs once after two colliders stop colliding (in that they stop touching). It can be triggered again with the same object if the objects collide again and stop touching.

<img src="Images\On Collision Enter 2D Node.png">

Inputs: 
Target (GameObject): If a GameObject is passed into this, the node will only execute when a collision with the specified GameObject is detected.

Outputs: 
- Trigger (Flow): The next node to execute.
- Collider (Collider 2D): The collider component of the colliding object.
- Contacts (Contact Point 2D Array): An array of [ContactPoint2D](https://docs.unity3d.com/6000.0/Documentation/ScriptReference/ContactPoint2D.html)s. These objects contain quite a bit of information, but most notably, they can tell you exactly where the collision occurred in world coordinates.
- Relative Velocity (Vector 2): The velocity of the collision. You can treat it like the force and direction of the collision.
- Enabled (Boolean): Whether a collision response is enabled or not.
- Data (Collision 2D): Contains all of the above information, plus a lot extra. All of it can be found [here](https://docs.unity3d.com/6000.0/Documentation/ScriptReference/Collision2D.html).

### On Stay 2D ##
This event occurs every physics timestep (by default, 50 times per second) while two colliders are touching.

<img src="Images\On Collision Stay 2D Node.png">

Inputs: 
Target (GameObject): If a GameObject is passed into this, the node will only execute when a collision with the specified GameObject is detected.

Outputs: 
- Trigger (Flow): The next node to execute.
- Collider (Collider 2D): The collider component of the colliding object.
- Contacts (Contact Point 2D Array): An array of [ContactPoint2D](https://docs.unity3d.com/6000.0/Documentation/ScriptReference/ContactPoint2D.html)s. These objects contain quite a bit of information, but most notably, they can tell you exactly where the collision occurred in world coordinates.
- Relative Velocity (Vector 2): The velocity of the collision. You can treat it like the force and direction of the collision.
- Enabled (Boolean): Whether a collision response is enabled or not.
- Data (Collision 2D): Contains all of the above information, plus a lot extra. All of it can be found [here](https://docs.unity3d.com/6000.0/Documentation/ScriptReference/Collision2D.html).

---
## Variable Nodes
Variables are a way to store/contain information in a script. They are a fundamental part of your scripts (and all of programming in general). Each variable has a type and a value. The type specifies the kind of data it can contain and the value is the data it does contain. There are also a number of scopes for you to use with your scripts. These determine where a variable can be accessed from.

Variables can be created and managed via the blackboard in the Script Graph window.

<img src="Images\Blackboard.png">

Common Types:
- Float: A number with decimal places. Can be positive or negative.
- Integer: A whole number. Can be positive or negative.
- String: Text data.
- Vector 2: A pair of floats. Intended to represent x and y values (for movement or positions).
- Game Object: Any GameObject.

Scopes: 
- Flow: Variables created within a graph. They cannot be created through the blackboard and only exist within the logical flow where they were created. To give an example, if you created a flow variable in the - - - On Update event, it would only be accessible in that On Update event after it was created. You likely won’t need to use these.
- Graph: Variables are only accessible within the graph they are associated with. They cannot be accessed by other graphs on the same object.
- Object: Variables are only accessible within the GameObject. If an object has multiple graphs, they will all be able to access these variables.
- Scene: Variables are accessible by all graphs within the same scene.
- App: Variables accessible throughout the entire game.
- Saved: These variables are also accessible throughout the entire scene. They persist, even after the game is closed. This can be used to create a basic save system.

Read more about variables [here](https://docs.unity3d.com/Packages/com.unity.visualscripting@1.9/manual/vs-variables.html).

### Get Variable ##
This node is used to read the value of a variable. At the top, there is a dropdown menu that allows you to select the scope you would like to get the variable from.

<img src="Images\Get Variable Node.png">

Inputs: 
- Name (String): The name of the variable to access.

Outputs: 
- Value (Object): The value of the variable being accessed.

### Set Variable ##
This node is used to change the value of a variable. At the top, there is a dropdown menu that allows you to select the scope you would like to get the variable from.

<img src="Images\Set Variable Node.png">

Inputs: 
- Assign (Flow): The node to execute before this one.
- Name (String): The name of the variable to access.
- New Value (Object): The value to change the variable to. Make sure the value is the correct type.

Outputs: 
- Assigned (Flow): The next node to execute.
- Value (Object): The value of the variable after setting it.

---
## Control Nodes
These nodes allow you to change the control flow of your scripts, allowing them to branch off and converge to do different things based on various conditions. Without them, your scripts would probably be a lot less responsive.

Read more about control nodes [here](https://docs.unity3d.com/Packages/com.unity.visualscripting@1.9/manual/vs-control.html).

### If Node ##
This node allows you to change the control flow based on a condition. Basically, that means you can create branching paths in your scripts. You can generally read an if statement as: “If the given condition is true, do something, otherwise, do something else.”

You do not necessarily need to assign both output pipes to any other nodes. If you don’t, the control flow will end if the script tries to go down the unassigned true/false path.

<img src="Images\If Node.png">

Inputs: 
- Enter (Flow): The node to execute before this one.
- Condition (Boolean): The condition used to choose between the two paths.

Outputs: 
- True (Flow): The next node to execute if the condition is true.
- False (Flow): The next node to execute if the condition is false.

### Select Node ##
This node outputs one of two values based on a condition. If the condition is true, it will output the first value passed in, if it’s false, it will output the other.

Both value inputs must be assigned some value, otherwise, this node will not work.

<img src="Images\Select Node.png">

Inputs: 
- Condition (Boolean): The condition used to choose the output.
- True (Object): The value to output if the condition is true.
- False (Object): The value to output if the condition is false.

Outputs: 
- Selection (Object): The value to output.

### For Loop Node ##
This node allows you to repeat a certain section of your graph a specified number of times. Anything attached to the body output will be repeated.

The way it works is that you provide it with a first value, last value and step value. It also separately keeps track of an index value (this can be accessed from the index output). The loop will then execute these steps:
1. Set the index value equal to the first value.
2. Check if the index is less than the last value.\
   a. If it is less, continue to step 3.\
   b. If it is greater than or equal to, the loop ends and the script executes the exit output.
3. The body output is executed once.
4. Add the step value to the index.
5. Repeat from step 2.

<img src="Images\For Loop Node.png">

Inputs: 
- Enter (Flow): The node to execute before this one.
- First (Integer): The starting value for the index.
- Last (Integer): The ending value for the index.
- Step (Integer): The amount to add to the index in each loop iteration.

Outputs: 
- Exit (Flow): The node to execute after the loop completes.
- Body (Flow): The node to execute each time the loop repeats.
- Index (Integer): The current index of the loop.

---
## Formula Nodes
These allow you to perform arithmetic within your graphs. There is a very large range of math nodes available to you, so it’s worth looking into, especially if you want to do things like custom physics.

Note that there are multiple variants of these nodes. We will generally be using the Math/Generic versions, which allows the use of any applicable data types (not just numbers). This means we can do things like concatenating strings or performing arithmetic with vectors.

Read more about formulae and arithmetic [here](https://docs.unity3d.com/Packages/com.unity.visualscripting@1.9/manual/vs-formula.html).

### Add Node ##
Allows you to add values together. Note that this node allows you to control the number of inputs to add together (up to 10) using the input field near the top of the node. None of the other Math/Generic nodes let you do this.

<img src="Images\Add Node.png">

Inputs: 
- A (Object): The first value to add.
- B (Object): The second value to add.
- C… J (Object): All other values to add.

Outputs: 
- Sum (Object): The result of the addition.

### Subtract Node ##
Allows you to subtract one value from another.

<img src="Images\Subtract Node.png">

Inputs: 
- A (Object): The value to subtract from.
- B (Object): The value to subtract.

Outputs: 
- A - B (Object): The result of the subtraction.

### Multiply Node ##
Allows you to multiply two values.

<img src="Images\Multiply Node.png">

Inputs: 
- A (Object): The first value to multiply.
- B (Object): The second value to multiply.

Outputs: 
- A x B (Object): The result of the multiplication.

### Divide Node ##
Allows you to divide one value by another.

<img src="Images\Divide Node.png">

Inputs: 
- A (Object): The value to divide.
- B (Object): The value to divide by.

Outputs: 
- A ÷ B (Object): The result of the division.

### Modulo Node ##
Allows you to perform modulo arithmetic. It divides the first term by the second and outputs the remainder. It’s useful for looping counters or screen wrapping.

<img src="Images\Modulo Node.png">

Inputs: 
- A (Object): The value to divide.
- B (Object): The value to divide by.

Outputs: 
- A % B (Object): The remainder after dividing.

---
## Transform
This component is responsible for the position, rotation and scale of your GameObjects. All GameObjects should have one automatically if they exist within a scene. It has quite a few nodes and functions for manipulating these three aspects of your objects.

Read more about the transform component [here](https://docs.unity3d.com/6000.0/Documentation/Manual/class-Transform.html).

### Get Position ##
Gets the specified object’s position in world space.

<img src="Images\Get Position Node.png">

Inputs: 
- Target (Transform): The object to get the position from.

Outputs: 
- Value (Vector3): The position of the object in world space.

### Get Local Position ##
Gets the specified object’s coordinate relative to its parent.

<img src="Images\Get Local Position Node.png">

Inputs: 
- Target (Transform): The object to get the position from.

Outputs: 
- Value (Vector3): The local position of the object.

### Get Rotation ##
Gets the specified object’s rotation in world space as a quaternion. A quaternion is basically just a representation of rotation.

You can convert a Euler angle to a quaternion through the Quaternion: Euler node.

<img src="Images\Get Rotation Node.png">

Read more about quaternions and Euler angles [here](https://docs.unity3d.com/6000.0/Documentation/Manual/QuaternionAndEulerRotationsInUnity.html).

Inputs: 
- Target (Transform): The object to get the rotation from.

Outputs: 
- Value (Quaternion): The rotation of the object in world space.

### Get Local Rotation ##
Gets the specified object’s rotation relative to its parent as a quaternion. A quaternion is basically just a representation of rotation.

You can convert a Euler angle to a quaternion through the Quaternion: Euler node.

<img src="Images\Get Local Rotation Node.png">

Read more about quaternions and Euler angles [here](https://docs.unity3d.com/6000.0/Documentation/Manual/QuaternionAndEulerRotationsInUnity.html).

Inputs: 
- Target (Transform): The object to get the rotation from.

Outputs: 
- Value (Quaternion): The rotation of the object relative to its parent.

### Get Local Scale ##
Gets the specified object’s scale relative to its parent. You may wonder why we don’t have a Get Scale node. It’s complicated, but the basic idea is that scale can be affected by rotation, so it cannot be properly represented as a Vector3. You can use the Transform: Get Lossy Scale node if you would like an approximation of scale in world space.

<img src="Images\Get Local Scale Node.png">

Inputs: 
- Target (Transform): The object to get the scale from.

Outputs: 
- Value (Vector3): The scale of the object relative to its parent.

### Set Position ##
Sets the specified object’s position in world space.

<img src="Images\Set Position Node.png">

Inputs: 
- Set (Flow): The node to execute before this one.
- Target (Transform): The object to set the position of.
- Value (Vector 3): The position to set the object to.

Outputs: 
- On Set (Flow): The next node to execute.
- Value (Vector 3): The position that the object was set to.

### Set Local Position ##
Sets the specified object’s coordinate relative to its parent.

<img src="Images\Set Local Position Node.png">

Inputs: 
- Set (Flow): The node to execute before this one.
- Target (Transform): The object to set the position of.
- Value (Vector 3): The position to set the object relative to its parent.

Outputs: 
- On Set (Flow): The next node to execute.
- Value (Vector 3): The position that the object was set, relative to its parent.

### Set Rotation ##
Sets the specified object’s rotation in world space using a quaternion. A quaternion is basically just a representation of rotation.

You can convert a Euler angle to a quaternion through the Quaternion: Euler node.

<img src="Images\Set Rotation Node.png">

Read more about quaternions and Euler angles [here](https://docs.unity3d.com/6000.0/Documentation/Manual/QuaternionAndEulerRotationsInUnity.html).

Inputs: 
- Set (Flow): The node to execute before this one.
- Target (Transform): The object to set the rotation of.
- Value (Quaternion): The rotation to set the object to.

Outputs: 
- On Set (Flow): The next node to execute.
- Value (Quaternion): The rotation that the object was set to.

### Set Local Rotation ##
Sets the specified object’s rotation relative to its parent using a quaternion. A quaternion is basically just a representation of rotation.

You can convert a Euler angle to a quaternion through the Quaternion: Euler node.

<img src="Images\Set Local Rotation Node.png">

Read more about quaternions and Euler angles [here](https://docs.unity3d.com/6000.0/Documentation/Manual/QuaternionAndEulerRotationsInUnity.html).

Inputs: 
- Set (Flow): The node to execute before this one.
- Target (Transform): The object to set the rotation of.
- Value (Quaternion): The rotation to set the object to, relative to its parent.

Outputs: 
- On Set (Flow): The next node to execute.
- Value (Quaternion): The rotation that the object was set to, relative to its parent.

### Set Local Scale ##
Sets the specified object’s scale, relative to its parent. There is no Set Scale function, but this node should cover all of your needs.

<img src="Images\Set Local Scale Node.png">

Inputs: 
- Set (Flow): The node to execute before this one.
- Target (Transform): The object to scale.
- Value (Vector 3): The scale to set the object to, relative to its parent.

Outputs: 
- On Set (Flow): The next node to execute.
- Value (Vector 3): The scale that the object was set to, relative to its parent.

### Translate ##
Moves a specified object by a certain distance. This differs from Set Position in that it moves an object from its current position, rather than teleporting it to a specific coordinate.

There are multiple variants of this node that allow for different inputs. The Transform: Translate (Translation, RelativeTo) variant will be described here.

<img src="Images\Translate Node.png">

Translation can be applied locally (self) or relative to the world. When translating locally, the direction the object is facing is taken into account, while when translating relative to the world, the object’s current direction does not matter and the object will move based on world coordinates.

<img src="Images\LocalVsWorldTranslation.png">

Inputs: 
- Invoke (Flow): The node to execute before this one.
- Target (Transform): The object to move.
- Translation (Vector 3): The direction and distance to move the object.
- Relative To (Space): Whether to move relative to self or world.

Outputs: 
- Exit (Flow): The next node to execute.

### Rotate ##
Applies a rotation to a specified object. As we’re only working in Unity 2D for this unit, we will generally only need to modify an object’s rotation around the z-axis. This differs from Set Rotation in that it rotates the object from its current position, rather than setting its rotation to a specific value.

There are multiple variants of this node that allow for different inputs. The Transform: Rotate (Eulers, RelativeTo) variant will be described here.

<img src="Images\Rotate Node.png">

Rotation can be applied locally (self) or relative to the world. When rotating locally, the direction the object is facing is taken into account, while when rotating relative to the world, the object’s current direction does not matter and the object will rotate based on world coordinates.

Inputs: 
- Invoke (Flow): The node to execute before this one.
- Target (Transform): The object to rotate.
- Eulers (Vector 3): The rotation to apply in degrees on each axis. You will generally only need to modify the rotation around the z-axis (the third number in the Vector 3).
- Relative To (Space): Whether to rotate relative to self or world.

Outputs: 
- Exit (Flow): The next node to execute.

---
## Time
The time class allows you to interact with many different aspects of time within your games, like seeing how long your levels have been loaded for or checking framerate information. We won’t be using too much of that outside of delta time, but it’s worth being aware of its existence.

### Get Delta Time
Allows you to check the time interval between frames. Frame rate can be variable (as you may have experienced if you have a not-so-up-to-date PC and are trying to play an intensive game), so making things dependent on it can lead to unexpected behaviours at different frame rates, like the same characters/objects moving at different speeds or certain inputs and actions becoming impossible. Applying delta time to any frame rate-based actions (e.g. translating an object in the update event) will instead make them time-based and thus remove any frame rate discrepancies.

<img src="Images\Get Delta Time Node.png">

Inputs: 
None

Outputs: 
Float: Seconds since last frame.

Use Case Examples: 

---
## Vector2

A Vector 2 is a representation of a 2D direction or a point. It’s basically just a pair of numbers, representing an x and y value. Be sure to distinguish between vectors and coordinates, as Vector 2s are used to represent both. Vectors represent directions, while coordinates represent positions.

### Get Magnitude ##
Gets the magnitude of a Vector 2. The magnitude is the length of the vector, represented as a singular number.

<img src="Images\Get Magnitude Node.png">

Inputs: 
- Target (Vector 2): The vector to measure.

Outputs: 
- Value (Float): The magnitude of the vector.

### Get Normalized ##
Sets a vector’s magnitude to 1, whilst retaining its direction. We tend to want to normalise vectors when comparing or modifying them, as it brings them all to a consistent length while retaining their direction. Imagine trying to change the magnitude of a vector from 3.21511573 to 5. It would probably be easier to normalise it and multiply it by 5 than it would be to scale that starting value.

Note that this is specifically the Vector2: Get Normalised node. There are other similarly-named nodes that do different things.

<img src="Images\Get Normalized Node.png">

Inputs: 
- Target (Vector 2): The vector to normalise.

Outputs: 
- Value (Vector 2): The normalised vector.

### Rotate (Custom) ##

### IsOnLeft (Custom) ##

---
## Game Object
All objects that exist within a scene are Game Objects. This means these nodes are usable and applicable across all scene objects.

Read more about Game Objects [here](https://docs.unity3d.com/6000.0/Documentation/Manual/class-GameObject.html).

### Set Active ##
Sets the active state of an object. An inactive object will not be visible and its scripts and components will not function. If an object is a parent, its children will become active/inactive along with it.

<img src="Images\Set Active Node.png">

Inputs: 
- Invoke (Flow): The node to execute before this one.
- Target (Game Object): The Game Object to activate/deactivate.
- Value (Boolean): Determines whether the object will be active or inactive.

Outputs: 
- Exit (Flow): The next node to execute.

---
## Debug
This is a collection of functions and nodes to help visualise and debug your scripts in various ways. Oftentimes, large parts of your scripts may be completely opaque, making it very hard to understand what’s going on (though, this is largely alleviated by the visual nature of visual scripting). You can use these nodes to print things in the console or draw things on your screen.

### Log ##
Prints a specified object to the console. You can print anything, as long as it can be represented as text.

<img src="Images\Debug Log Node.png">

Inputs: 
- Invoke (Flow): The node to execute before this one.
- Message (Object): The object to print to the console.

Outputs: 
- Exit (Flow): The next node to execute.

---
## Input (Custom)

### Get Input Button

### Get Input Axis

### Get Input Vector2

