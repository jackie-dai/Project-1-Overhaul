## Section 7 - Interacting with pickups

In the previous section, we implemented the Interact() function for *Chest* that destroys the *Chest* game object and leaves in its place a *Health Potion*. 
As of right now, the function is not being used. Lets make use of it in the following section.

The `Interact()` function should be called whenever the player presses "E" on a chest.  

//note: change function name Interact() -> Open()

First, open up *PlayerController.cs* and add a conditional if statement inside the `Update()` function to repeatedly check if the player presses the "E" key. If the "E" key is pressed, call the *PlayerController*'s `Interact()` function; we  shall implement the functionality of this function in the next step.

Still inside *PlayerController* script, navigate down to the Interact() function. This function, when invoked, will check if the player is facing a chest, if so, it will call that particular `Chest` instance's `Interact()` function to drop a *Health Potion*.

**Task: Implement `Interact()`: use a `BoxCastAll` to check if the player is facing a `Chest` game object` if so, call that `Chest`'s `Interact()` function.**

Solution (translate hex to ascii):
```
68 74 74 70 73 3A 2F 2F 79 6F 75 74 75 2E 62 65 2F 4E 74 4F 54 70 67 44 4F 7A 49 30 3F 73 69 3D 52 44 43 64 6F 46 35 74 36 68 6A 77 39 44 30 4A 26 74 3D 37 31
```

