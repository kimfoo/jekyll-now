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

![grid](https://www.awesomeincu.com/img/tutorials/unity-pong/2d_button.png?raw=true)

7. Unzip Unity Pong Assets file. Click and drag all files into the project pane below your scene view.

![assets](https://www.awesomeincu.com/img/tutorials/unity-pong/unitypong-assets.png?raw=true)

8. Drag the background image 'Background.jpg' to the hierarchy pane, just below the main camera.
9. If image is not centered, change Transform Position to (0,0,0).
10. Select 'Background', and you should see the Inspector Pane.
11. Under Transform, change the scale to (0.75,0.75,1).
12. Go to 'Sprite Renderer'> 'Sorting Layer'> click 'Add Sorting Layer'.
13. Click the + icon to add our new layer. Change its name from ‘New Layer’ to ‘Background’, then click and drag our new layer above the Default layer.
14. Re-select your Background object in the Hierarchy pane so that it will show up in the Inspector again. 
15. In 'Sprite Renderer'> Sorting Layer> choose 'Background Layer'

16. Select the Main Camera object in your Hierarchy pane. 
17. Under 'Camera' component, change 'Size' to 3. 
18. Click on 'Background' property, in the color picker, choose the color black, with RGBA values of (0,0,0,0).

```C#
void Start () {
    theBall = GameObject.FindGameObjectWithTag("Ball");
}
```
