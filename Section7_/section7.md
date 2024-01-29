## Section 7 - Interacting with pickups

In the previous section, we just implemnented the Interact() function for *Chest*, which destroys the *Chest* game object and leaves in its place a *Health Potion*. Now, we just have to keep checking if the player pressed the "E" key. 

In *PlayerController* write a if statement inside `Update()` to check when the player presses the "E" key. Then, call the *PlayerController*'s `Interact()` function that we shall implement next.

*PlayerController*'s Interact() function, when invoked, will check if the player is facing a chest, if so, it will call that particular `Chest` instance's `Interact()` function to drop a *Health Potion*.

**Task: Implement `Interact()`: use a `BoxCastAll` to check if the player is facing a `Chest` game object` if so, call that `Chest`'s `Interact()` function.

