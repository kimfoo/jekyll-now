---
layout: page
title: 2D Pong Game Creation
permalink: /2D Pong Game Creation/
---



Today, the name of the game is Pong. We’re going to be using Unity v5.6 or later, and we’ll use C# as our coding language. No prior experience with Unity or C# is required. It will only take you about 1.5 hours to complete the tutorial, and at the end you’ll have made your own version of Pong!

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
```cs
public class PlayerControls : MonoBehaviour {
```
3. The next few lines are variables we need to write ourselves. The first two lines we add will denote the keys that we’ll press to move the paddles (W goes up, S goes down), and the next one is the speed of the paddle. The ‘boundY’ variable is the highest position that we want our paddle to go. This keeps it from moving off the edges of the screen. The last variable is a reference to our Rigidbody that we’ll use later.
```cs
public KeyCode moveUp = KeyCode.W;
public KeyCode moveDown = KeyCode.S;
public float speed = 10.0f;
public float boundY = 2.25f;
private Rigidbody2D rb2d;
```
4. By making these variables ‘public,’ we can adjust them through our Unity interface as well. If we have variables we don’t want other developers to see in the Unity interface, we should call them ‘private’.
5. Start() is a function that is called when we first launch our game. We’ll use it to do some initial setup, such as setting up our Rigidbody2D:
```cs
void Start () {
    rb2d = GetComponent<Rigidbody2D>();
}
```
5. Update() is a function that is called once per frame. We’ll use it to tell us what button is being pressed, and then move the paddle accordingly, or, if no button is pressed, keep the paddle still. Lastly we’ll bound the paddle vertically between +boundY and -boundY, which will keep it inside the game screen at all times.
```cs
void Update () {
    var vel = rb2d.velocity;
    if (Input.GetKey(moveUp)) {
        vel.y = speed;
    }
    else if (Input.GetKey(moveDown)) {
        vel.y = -speed;
    }
    else if (!Input.anyKey) {
        vel.y = 0;
    }
    rb2d.velocity = vel;

    var pos = transform.position;
    if (pos.y > boundY) {
        pos.y = boundY;
    }
    else if (pos.y < -boundY) {
        pos.y = -boundY;
    }
    transform.position = pos;
}
```
6. Save and exit.
7. To test our game, click the play button (►) at the top of the screen. Use the W and S keys to move. Does it work? Awesome!

    <p align="center">
          <img src="https://www.awesomeincu.com/img/tutorials/unity-pong/playmode.png?raw=true">
        </p>
        
8. Try clicking the Player01 object in the Hierarchy and changing the position of the paddle in the Inspector while the game is running in Play Mode. This is super handy for trying out new ideas in real time. Warning: *The changes you make during Play Mode do not stay when you close Play Mode.*
9. The next step is to make a second paddle. All we need to do is right click ‘Player01’ in the Hierarchy menu, and choose Duplicate from the menu that appears when we right click. Rename it to be ‘Player02’.
10. Next, change its key bindings (recommend using ‘Up Arrow’ for up and ‘Down Arrow’ for down), and move it to be the opposite location on the board - change the X value in its Transform Position to be positive. Player01 should be on the left, Player02 on the right. Now go to ‘Game’ and test this one too. 

    <p align="center">
          <img src="https://www.awesomeincu.com/img/tutorials/unity-pong/image_12.png?raw=true">
        </p>

## Step 3 : The Ball

1. Find the Ball image in the Project pane. Drag the Ball into the Scene, same as our Paddles. There should now be an object in the Hierarchy pane named ‘Ball’. Click on it, then head over to the Inspector pane to get the ball rolling. 
2. First, add a custom Tag called “Ball”, then go back and assign this new tag to our Ball. (This process is just like when you added a Sorting Layer to your background, except you click ‘Add Tag’ instead of ‘Add Sorting Layer’.)

     <p align="center">
          <img src="https://www.awesomeincu.com/img/tutorials/unity-pong/assign_ball_tag.png?raw=true">
        </p>

3. Next, change the scale of our ball to (0.5, 0.5, 1). 
4. Click the Add Component button, then in Physics 2D, let’s add ‘Circle Collider 2D’ and of course ‘Rigidbody 2D.’ In the Circle Collider, change the Radius to 0.23. 
5. Now we are going to apply a Physics 2D Material. To apply the material, select ‘Ball’ in the inspector. Drag ‘BallBounce’ to the ‘Circle Collider 2D’ box. We also need to adjust several settings in ‘Rigidbody 2D’ so we can get our desired pong ball behavior. It should look like this at the end:

     <p align="center">
          <img src="https://www.awesomeincu.com/img/tutorials/unity-pong/ball_inspector_physics.png?raw=true">
        </p>
        
6. With ‘Ball’ still selected in your Hierarchy, click Add Component in the Inspector pane. Create a New Script, this time called ‘BallControl’, with the C Sharp language selected. 
7. Double click on the new BallControl script to open it in MonoDevelop. 

### Code Breakdown

1. First, as always, we import our packages and confirm that our class name matches our filename.
```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
public class BallControl : MonoBehaviour {
```
2. Declare these variables.
```cs
private Rigidbody2D rb2d;
private Vector2 vel;
```
3. We also need a GoBall() function, that will choose a random direction (left or right), then make the ball start to move.
```cs
void GoBall(){
    float rand = Random.Range(0, 2);
    if(rand < 1){
        rb2d.AddForce(new Vector2(20, -15));
    } else {
        rb2d.AddForce(new Vector2(-20, -15));
    }
}
```
4. In our Start() function, we’ll initialize our rb2d variable. Then we’ll call the GoBall() function, using Invoke(), which allows us to wait before execution. This will wait two seconds to give players time to get ready before the ball starts moving.
```cs
void Start () {
    rb2d = GetComponent<Rigidbody2D>();
    Invoke("GoBall", 2);
}
```
5. ResetBall() and ResartGame() are two functions used by other scripts which we will write later. ResetBall() is used when a win condition is met. It stops the ball, and resets its position to the center of the board.
```cs
void ResetBall(){
    vel = Vector2.zero;
    rb2d.velocity = vel;
    transform.position = Vector2.zero;
}
```
6. RestartGame() is used when our restart button is pushed. We’ll add that button later. This function uses ResetBall() to center the ball on the board. Then it uses Invoke() to wait 1 second, then start the ball moving again.
```cs
void RestartGame(){
    ResetBall();
    Invoke("GoBall", 1);
}
```
7. OnCollisionEnter2D() waits until we collide with a paddle, then adjusts the velocity appropriately using both the speed of the ball and of the paddle.
```cs
void OnCollisionEnter2D (Collision2D coll) {
    if(coll.collider.CompareTag("Player")){
        vel.x = rb2d.velocity.x;
        vel.y = (rb2d.velocity.y / 2.0f) + (coll.collider.attachedRigidbody.velocity.y / 3.0f);
        rb2d.velocity = vel;
    }
}
```

## Step 4 : The Walls

1. Make sure nothing is selected in the Hierarchy pane, then right click some empty space in the Hierarchy and choose ‘Create Empty’. Also, make sure that it has a position of (0,0,0).
2. In the Hierarchy pane, right click on the ‘Walls’ object we just made and choose ‘Create Empty’. This will make a new game object that is a ‘child’ of the Walls object. Call this new child object ‘RightWall.’ 
3. Go to ‘AddComponent’ and add a Box Collider 2D.

    <p align="center">
          <img src="https://www.awesomeincu.com/img/tutorials/unity-pong/rightwall.png?raw=true">
        </p>

4. Duplicate our new wall object 3 times. Call those duplicates ‘LeftWall’, ‘TopWall’, and ‘BottomWall’.
* RightWall: Position(5.8, 0, 0)  ,  Scale(1, 6, 1)
* LeftWall: Position(-5.8, 0, 0)  ,  Scale(1, 6, 1)
* TopWall: Position(0, 3.5, 0)  ,  Scale(10.7, 1, 1)
* BottomWall: Position(0, -3.5, 0)  ,  Scale(10.7, 1, 1)

    <p align="center">
          <img src="https://www.awesomeincu.com/img/tutorials/unity-pong/walls_sceneview.png?raw=true">
        </p>
        
5. Now hit play (►), and the ball will bounce off the walls!


## Step 5 : The Scoring User Interface

1. First things first, we need a game object for our HUD (or Heads-Up Display). Right click an empty space in the Hierarchy pane and choose ‘Create Empty’. 
2. Call the new object ‘HUD’, center its position at (0, 0, 0), and add a new script to the HUD object called ‘GameManager’.

### Code Breakdown

1. First, as always, we import our packages and declare our class.
```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
public class GameManager : MonoBehaviour {
```
2. Next, we make 4 variables.
```cs
public static int PlayerScore1 = 0;
public static int PlayerScore2 = 0;
public GUISkin layout;
GameObject theBall;
```
3. Then comes the Start() function, which we use when the game first starts.
```cs
void Start () {
    theBall = GameObject.FindGameObjectWithTag("Ball");
}
```
4. Next is the Score() function. It will get called by another script we write in just a minute, that detects when the ball hits the side walls.
```cs
public static void Score (string wallID) {
    if (wallID == "RightWall")
    {
        PlayerScore1++;
    } else
    {
        PlayerScore2++;
    }
}
```
5. The OnGUI() function takes care of displaying the score and the reset button functionality. Then, it checks every time something happens if someone has won yet, and triggers the function ResetBall() if someone has.
```cs
void OnGUI () {
    GUI.skin = layout;
    GUI.Label(new Rect(Screen.width / 2 - 150 - 12, 20, 100, 100), "" + PlayerScore1);
    GUI.Label(new Rect(Screen.width / 2 + 150 + 12, 20, 100, 100), "" + PlayerScore2);

    if (GUI.Button(new Rect(Screen.width / 2 - 60, 35, 120, 53), "RESTART"))
    {
        PlayerScore1 = 0;
        PlayerScore2 = 0;
        theBall.SendMessage("RestartGame", 0.5f, SendMessageOptions.RequireReceiver);
    }

    if (PlayerScore1 == 10)
    {
        GUI.Label(new Rect(Screen.width / 2 - 150, 200, 2000, 1000), "PLAYER ONE WINS");
        theBall.SendMessage("ResetBall", null, SendMessageOptions.RequireReceiver);
    } else if (PlayerScore2 == 10)
    {
        GUI.Label(new Rect(Screen.width / 2 - 150, 200, 2000, 1000), "PLAYER TWO WINS");
        theBall.SendMessage("ResetBall", null, SendMessageOptions.RequireReceiver);
    }
}
```
6. In your Project pane, right click and create a GUI Skin called ‘ScoreSkin’.
7. Click on that Skin, and you should see a variable field called ‘Font’ at the top of the Inspector pane. Click + drag our font to that variable slot.

    <p align="center">
          <img src="https://www.awesomeincu.com/img/tutorials/unity-pong/score_skin.png?raw=true">
        </p>
8. If you scroll down and look under the dropdown menus for ‘Label’ and ‘Button’ you can also change the size of your text, etc. Play around with size until it looks good.
9.  In the end, your HUD’s Game Manager (Script) should look like this:

   <p align="center">
          <img src="https://www.awesomeincu.com/img/tutorials/unity-pong/game_manager_layout.png?raw=true">
        </p>

10. Now, when you play, you should see something like this:

    <p align="center">
          <img src="https://www.awesomeincu.com/img/tutorials/unity-pong/gui_font_enabled.png?raw=true">
        </p>
        
11. Now let’s make sure that the game knows when we do score. To do that, we need to add a script to the ‘LeftWall’ and ‘RightWall’ objects under the HUD dropdown. Go to ‘Add Component’ on the LeftWall, and name this new script ‘SideWalls.cs’.

### Code Breakdown

1. We will now write a function that detects when something is colliding with our left or right walls. If it’s the ball, we call the score method in GameManager, and reset the ball to the middle. Add this script to LeftWall.
```cs
using UnityEngine;
using System.Collections;
public class SideWalls : MonoBehaviour {
    void OnTriggerEnter2D (Collider2D hitInfo) {
        if (hitInfo.name == "Ball")
        {
            string wallName = transform.name;
            GameManager.Score(wallName);
            hitInfo.gameObject.SendMessage("RestartGame", 1.0f, SendMessageOptions.RequireReceiver);
        }
    }
}
```
2. Go to ‘Add Component’ on ‘RightWall’ and choose just ‘Script’ instead of ‘New Script.’ Choose the Script we just wrote.
3. Now, in order for Unity to call our OnTriggerEnter2D method, we have to make sure both the LeftWall and RightWall have the “Is Trigger” checkbox selected on their Box Colliders in the Inspector pane. 
 
     <p align="center">
          <img src="https://www.awesomeincu.com/img/tutorials/unity-pong/istrigger.png?raw=true">
        </p>

4. Test your game to make sure both players can score a point. We're almost done!

## Last Step : Make The Game

1. Go to File at the top of Unity. Go to ‘Build Settings’ and then choose ‘Mac, PC, Linux Standalone.’ This will make an executable (playable) file appear on our desktop. You may need to ‘Add Open Scenes’, to ensure that Main is included in the build.
2. Now, click on ‘Player Settings.’ This is where you should put your name on the Project, choose an icon (Ball Sprite etc.), and uncheck ‘Default Is Full Screen’.
3. Set 960x540 as default screen width and height.
4. In the ‘Supported Aspect Ratios’ list, click the little arrow and uncheck everything except 16:10 and 16:9. If we choose a different aspect ratio, it’s possible we might not see our paddles. Your settings in the end should look like this:

    <p align="center">
          <img src="https://www.awesomeincu.com/img/tutorials/unity-pong/player_settings.png?raw=true">
        </p>
5. Hit Build and choose where you want to save the file, and name it Pong v1.0. 

#### Congratulations! Enjoy the game :)
    
  <p align="center">
          <img src="https://www.awesomeincu.com/img/tutorials/unity-pong/finished_pong_game.png?raw=true">
        </p>

     
## Bonus Last Step!!! (Optional)

### Deployment to Microsoft Azure

After completing your game, there is one last step which might be necessary depending on if you would like to share the game with others who do not have Unity installed on their laptop. Hosting your game on Microsoft Azure lets you do just that, minus the fuss of setting up a game server!

Please browse this [Microsoft Developer website](https://blogs.msdn.microsoft.com/uk_faculty_connection/2017/10/09/hosting-your-unity-game-on-azure/) for a step-by-step guide on hosting your Unity game on Microsoft Azure. Set up your Microsoft Azure account, make sure you have Microsoft Visual Studio 2017 installed, and you are ready to go.

*Remark: Please take note that this guide was made with Microsoft Visual Studio 2015. There are some minor differences in the interface, which means that you will not be able to select "New Website" in File. Instead, go to **File > Open > Website and select the folder in which your Unity WebGL version of your game is located. Then, proceed to continue at Step 9 onwards of the step-by-step guide.**

















