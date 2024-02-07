## Section 8: Menu Screens

Now that the core gameplay has been implemented, we can now round off our game with menu screens that allow the player to navigate from opening the game to playing it and vice versa. Menu screens are a quick way to add polish to your game and improve the user experience, as well as enforcing the style or theme that your game is going for.

{: .note}
> Make sure you are constantly saving your project using either ctrl+s or File > Save whenever you make changes to it. Unity can crash at any time, so saving frequently can reduce the damage done to your progress when these unlikely scenarios may occur.

## Main Menu
Head to the Scenes folder in the Inspector, and right click to create a new scene with Create > Scene. Name this scene “MainMenu”, and open the scene. Create a canvas (this will also make an EventManager), and name it “MainMenuCanvas”. 

Create a Text object under the new canvas and name it “TitleText”. Increase the font size to 40, change both alignments to the centered option, and change both Horizontal Overflow and Vertical Overflow to “Overflow”. Change the text to your game’s title. (You can choose this name! If you don’t care, call it Awesome Game) 

Create an Image under MainMenuCanvas and drag it above TitleText in the Hierarchy. Notice how the image moves behind the text in the Game view. Click on the Anchor Preset box on the top left of the RecTransform component and click on the bottom right box with 4 blue arrows extending outwards. Change the Left, Right, Top, and Bottom transforms to 0 to stretch the image toward the edges of the screen.

![disable view](images/fig8.1.png)

Change the Color of the image to your choice of background color. Add a Button object to the MainMenuCanvas and lower the button either in the scene or by changing the Y position to -75 in the Inspector. Access the Text object, the child of Button, and change the text to “Start Game.”

## Win and Lose Screens

Task: Create two more scenes, “WinScene” and “LoseScene”, that will show up when the win and lose conditions are met respectively.

Note: Both scenes, at minimum, will have the same components as the “MainMenu” scene, so you can use the “Duplicate Scene” function to save some time. Make sure to change the components and rename the scene so that they are distinct from the main menu.


``` 
68 74 74 70 73 3A 2F 2F 79 6F 75 74 75 2E 62 65 2F 41 33 78 35 69 50 6A 36 6A 6C 63 3F 6C 69 73 74 3D 50 4C 6B 54 71 66 35 44 42 7A 50 73 41 65 2D 70 52 35 62 44 55 64 77 48 69 43 4E 67 48 63 79 42 49 68 26 74 3D 34 39 
```

## Scene Management

To hold all of the scene management code, we will be using a GameManager script. The GameManager script is typically where, as the name suggests, most of the game management code is stored. Since most of the code that maintains the gameplay has been delegated to other scripts, this GameManager script will control scene management.

Create an empty GameObject and name it “GameManager”. Create the tag “GameController” and assign it to the GameManager. This is so we can reference the GameObject more easily in later scripts. Open the GameManager.cs script and take a look at the code below:

```
using UnityEngine.SceneManagement;

public static GameManager Instance = null;

#region Unity_functions

private void Awake()
{
    if (Instance == null)
	{
		Instance = this;
	} else if (Instance != this) {
		Destroy(this.gameObject);
	}
	DontDestroyOnLoad(gameObject);
}

#endregion
```

- Importing the SceneManagement package allows us to access specific functions to move between scenes in the game
- The if block checks if a GameManager script exists already:
    - If it doesn’t, it assigns itself to a reference that can be accessed in other scripts.
    - If it does, it destroys itself, the GameObject, to prevent itself from overwriting the existing GameManager.
- After the if statement, it makes sure that the GameManager is not deleted when the game switches between scenes, so that scripts can continue to reference GameManager.

Why put so much effort into maintaining a proper GameManager script? GameObjects are typically not supposed to persist between scenes unless directed by the line “DontDestroyOnLoad(gameObject)”. However, the GameManager script tends to hold important variables that correspond to all parts of the game, from scores to player information and even sound settings. Keeping a single version of the GameManager script lets the game retain its own information so that it can be used all throughout the game’s different scenes.

Once you’ve looked at the code above, scroll down to the Scene_transitions region containing four empty functions; “StartGame()”, “LoseGame()”, “WinGame()”, and “MainGame()”. Each of these functions will run whenever a scene change is needed.

Task: Using SceneManager.LoadScene(string sceneName), fill in these four functions so that the game is directed to the correct scene as depicted by the function’s name.

Note: Each function should load to a different scene. Scene names are also CASE SENSITIVE, so double-check your spelling and cases first if you run into issues.

```
 68 74 74 70 73 3A 2F 2F 79 6F 75 74 75 2E 62 65 2F 78 44 64 31 50 46 44 7A 4E 57 55 3F 6C 69 73 74 3D 50 4C 6B 54 71 66 35 44 42 7A 50 73 41 65 2D 70 52 35 62 44 55 64 77 48 69 43 4E 67 48 63 79 42 49 68 26 74 3D 32 30 37 
```

You have successfully implemented the necessary functions within GameManager.cs to navigate through the UI! Attach GameManager.cs to the GameManager object and turn the object into a prefab.

We will now hook up the functions to the buttons in each scene. Access the StartButton object under MainMenuCanvas and scroll to the Button component, where you’ll find an OnClick() box. Click the plus sign at the bottom right so that the box looks like the figure below. If it already looks like the figure, you do not need to add a second function.

![disable view](images/fig8.2.png)

Drag the GameManager prefab into the empty object slot, and select GameManager > StartGame() on the dropdown menu. Now when the button is clicked, the StartGame() function will execute.

An important step is to head to File > Build Settings and click on the Add Open Scenes button under Scenes In Build. This will add MainMenu to the build, which will allow SceneManager to access the scene in order to switch to it.

{: .important}
> SceneManager functions can only access scenes that are contained in the build. Add scenes that you want to access into the build before testing out the SceneManager functions.

Run the scene and click on the Start Game button, ensuring that the game transitions into the main game scene, or SampleScene. Go ahead and switch to the other scenes as well and make sure that their respective buttons move to the right scenes.

Now, we will implement the rest of the transition functions. Open EndTriggerScript.cs and look at the method below:

```
private void OnTriggerEnter2D(Collider2D coll)
{
	if (coll.CompareTag(“Player))
	{
		gameObject gm = GameObject.FindWithTag(“GameController”);
		gm.GetComponent<GameManager>().WinGame();
	}
}
```

Since EndTriggerScript.cs is attached to an invisible GameObject with a BoxCollider2D component, the method OnTriggerEnter2D concludes the game when the player reaches the goal.
First, it searches the Hierarchy for a GameObject with the “GameController” tag. The only GameObject that should have this tag is the GameManager object.
Afterwards, it accesses WinGame() from GameManager.cs, thereby moving the scene to WinScene.

- Using this method of ending the game, implement a lose condition in Health.cs. 


``` 
68 74 74 70 73 3A 2F 2F 79 6F 75 74 75 2E 62 65 2F 41 69 68 54 49 45 32 67 2D 6C 55 3F 6C 69 73 74 3D 50 4C 6B 54 71 66 35 44 42 7A 50 73 41 65 2D 70 52 35 62 44 55 64 77 48 69 43 4E 67 48 63 79 42 49 68 26 74 3D 35 38 
```

Give yourself a pat on the back! You have a working game in your hands. Export the game through File > Build Settings... and press Build after checking that all scenes have been added to the build. A zip file containing your game will be created, and you can upload this file to the submission form for us to grade.
