---
layout: page
title: 2D Pong Game Creation
permalink: /2D Pong Game Creation/
---



Today, the name of the game is Pong. We’re going to be using Unity v5.6 or later, and we’ll use C# as our coding language. No prior experience with Unity or C# is required. It will only take you about two hours to complete the tutorial, and at the end you’ll have made your own version of Pong!

So, when we think about making Pong, we might think of several simple mechanics that need to be created:

1. You have a Background to play on
2. You have a set of Paddles that go up and down
3. You have a ball that bounces off walls and paddles
4. You have a set of side walls that you hit to score
5. You have a score at which you win
6. You have a rage quit button (or reset button)

## Step 1 : The Setup

1. From the welcome screen, click ‘Projects’. (If the Unity editor is already open, click ‘File’ > ‘New Project’ instead.) 
2. Name the project something like 'Pong Game'.
3. Choose '2D'
4. Set the 'Enable Unity Analytics' to off.
5. Hit 'Create Project'.
![newproject](https://www.awesomeincu.com/img/tutorials/unity-pong/new_project.png?raw=true)
6. Once the project is created, you should see a 2D grid appear in the scene   view. If you don’t, make sure the ‘2D’ button is pressed along the top toolbar of Scene view. (You can see it highlighted in yellow in this image.)

    <p align="center">
      <img src="https://www.awesomeincu.com/img/tutorials/unity-pong/2d_button.png?raw=true">
    </p>

7. Unzip Unity Pong Assets file. Click and drag all files into the project pane below your scene view.

    <p align="center">
      <img src="https://www.awesomeincu.com/img/tutorials/unity-pong/unitypong-assets.png?raw=true">
    </p>

    <p align="center">
      <img src="https://www.awesomeincu.com/img/tutorials/unity-pong/background_project_pane.png">
    </p>

8. Drag the background image 'Background.jpg' to the hierarchy pane, just below the main camera.

    <p align="center">
      <img src="https://www.awesomeincu.com/img/tutorials/unity-pong/background_hierarchy_pane.png">
    </p>

9. If image is not centered, change Transform Position to (0,0,0).
10. Select 'Background', and you should see the Inspector Pane.
11. Under Transform, change the scale to (0.75,0.75,1).
12. Go to 'Sprite Renderer'> 'Sorting Layer'> click 'Add Sorting Layer'.

    <p align="center">
      <img src="https://www.awesomeincu.com/img/tutorials/unity-pong/sorting_layer.png?raw=true">
    </p>

13. Click the + icon to add our new layer. Change its name from ‘New Layer’ to ‘Background’, then click and drag our new layer above the Default layer.
14. Re-select your Background object in the Hierarchy pane so that it will show up in the Inspector again. 
15. In 'Sprite Renderer'> Sorting Layer> choose 'Background Layer'

    <p align="center">
      <img src="https://www.awesomeincu.com/img/tutorials/unity-pong/background_sorting_layer.png?raw=true">
    </p>

16. Select the Main Camera object in your Hierarchy pane. 
17. Under 'Camera' component, change 'Size' to 3. 
18. Click on 'Background' property, in the color picker, choose the color black, with RGBA values of (0,0,0,0). The camera component should look like this:

    <p align="center">
      <img src="https://www.awesomeincu.com/img/tutorials/unity-pong/main_camera_inspector.png?raw=true">
    </p>

19. Now it is time to save your scene. Go to File -> Save Scene As… 'Main" in your Assets folder. Once you save, you should see a file called Main.unity from your Project pane.

    <p align="center">
      <img src="https://www.awesomeincu.com/img/tutorials/unity-pong/saved_scene_main.png?raw=true">
    </p>

## Step 2 : The Paddles

1. Find the image called ‘PongPaddle’ in the Assests folder, within your Project pane.
2. Now drag the paddle onto the scene in scene view. A ‘Player’ object should appear in your Hierarchy menu. Rename that to Player01. Click on it.
3. Over in the Inspector, click the Tag dropdown and select ‘Player’. Set Position to (X, Y, Z) = (-4, 0, 0) and Scale to (0.5, 1.5, 1). It should look like this in the Inspector:

     <p align="center">
          <img src="https://www.awesomeincu.com/img/tutorials/unity-pong/inspector_4.png?raw=true">
        </p>
       
4. Next we’re going to add two components to the Player object. Click on the ‘Add Component’ button, and then on ‘Physics 2D.’ 
5. Once you’ve done that add both a ‘Box Collider 2D’ and a ‘Rigidbody 2D.’ The Box Collider 2D is to make sure the ball will bounce off your paddle, and the Rigidbody 2D is there so we can move the paddle around. Note: It’s important to use Physics, BoxCollider, and RigidBody 2D here because 3D versions of those exist - that’s not what we want in our 2D game though.
6. Click the ‘Body Type’ dropdown menu and select ‘Kinematic’. Your Inspector should now look like this:

      <p align="center">
          <img src="https://www.awesomeincu.com/img/tutorials/unity-pong/player01_physics.png?raw=true">
        </p>
       
7. Now we are going to add a Script for movement for our paddles. Make sure that Player01 is still selected in your Hierarchy pane, then go to ‘Add Component’, and then ‘New Script.’
8. Call this one ‘PlayerControls’ and make sure the language is C# (or CSharp, as it is spelled out in Unity). Hit ‘Create and Add’.
9. Double click the icon that appears below in the Project pane to open it up in MonoDevelop, Unity’s Integrated Development Environment (or IDE) - essentially, it’s the program we use to write Unity scripts.

      <p align="center">
          <img src="https://www.awesomeincu.com/img/tutorials/unity-pong/image_6.png?raw=true">
        </p>

### Code Breakdown

1. The first three lines are packages of pre-written code we want to tell our program it can use.
```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
```

2. The next line is the class name, the name of our file. It’s the same thing that we named our Component.
```C#
public class PlayerControls : MonoBehaviour {
```

3. The next few lines are variables we need to write ourselves. The first two lines we add will denote the keys that we’ll press to move the paddles (W goes up, S goes down), and the next one is the speed of the paddle. The ‘boundY’ variable is the highest position that we want our paddle to go. This keeps it from moving off the edges of the screen. The last variable is a reference to our Rigidbody that we’ll use later.
```C#
public KeyCode moveUp = KeyCode.W;
public KeyCode moveDown = KeyCode.S;
public float speed = 10.0f;
public float boundY = 2.25f;
private Rigidbody2D rb2d;
```

4. By making these variables ‘public,’ we can adjust them through our Unity interface as well. If we have variables we don’t want other developers to see in the Unity interface, we should call them ‘private’.





