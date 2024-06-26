## Section 6 - Pickups

In this section, you will implement a chest object and a health potion object, then program the functionality to open these chests and receive health potions.

#### Summary:

1. Create a health potion GameObject that heals the player's health when the player walks over it
2. Create a chest that drops health potions when the player opens it

## Setting Up  Chest and HealthPack
Right click in the hierarchy to create a new sprite GameObject `2D Object > Sprite` and rename it to `Chest`. Then, follow these steps: 

1. In your project's directory, navigate to `Assets > Sprites > Items` and drag the *chest* sprite into the *SpriteRenderer* component's *Sprite* box. Alternatively, you can click on the circle next to the *Sprite* box and search the name *chest*.

2. Inside the *SpriteRenderer* component, look under "Additional Settings", set the *Sorting Layer* to *Enemy*.

{. note}
> We are setting the sorting layer to Enemy so the chest sprite appears above the environment layer

![](./images/fig6.1.png) Fig 6.1

3. Add a *Rigidbody2D* component and a *BoxCollider2D* component. Change the *Rigidbody 2D*'s body type to **Kinematic**. Kinematic means this game object is unaffected by gravity and can only be moved by script manipulation. **Additionally, freeze both x and y positions as well as the z rotation.**

![](./images/fig6.2.png) Fig 6.2

Now, create another sprite GameObject and name it *HealthPotion*. Repeat the following steps above for *HealthPotion*, **while making sure to check the *IsTrigger* checkbox under the *BoxCollider2D* component.**

### Health Pack Script

Navigate to the Scripts folder `Assets > Scripts` and attach the *HealthPotion.cs* script to your *HealthPotion* GameObject. Double click the script to edit it. 

```
#region HealthPotion_variables
[SerializeField]
[Tooltip("amount the player heals")]
private int healAmount;
#endregion
```

- `healAmount` will be the amount of health recovered once the user walks over the health potion.
- `ToolTip` will display the message it holds when the user hovers over the healAmount variable in the unity inspector

When a player walks over a health potion, it should boost their health points and disappear; signaling to the player that the potion has been used. 

**Task 6.1: In *HealthPotion.cs* fill in the `OnTriggerEnter2D()` function so the player gains `healAmount` of health when collided with. Add the potion sound to your script as well.**

Functions to modify:

*HealthPack.cs* -> `OnTriggerEnter2D()`

Solution (translate hex to ASCII):
```
68 74 74 70 73 3A 2F 2F 79 6F 75 74 75 2E 62 65 2F 50 6C 77 31 4F 30 55 75 5F 7A 51 3F 73 69 3D 66 74 31 61 6D 35 71 64 4F 6C 6E 77 58 37 70 52 26 74 3D 32 37 39
```

Attach the *HealthPack.cs* script to your `HealthPotion` GameObject. You can test out your implemention by using a `Debug.Log()` statement to print out your `currHealth` inside *PlayerController.cs*'s `Heal()` function and walking over the health potion with your player.

Finally, drag your *HealthPotion* GameObject into `Assets > Prefabs` to turn it into prefab.

## Chest Script

Change the *Chest* GameObject's tag to **Chest**. Navigate to the Scripts folder again and add the *Chest.cs* script to your *Chest* GameObject. Double click the script to edit it.

{: .note}
> Notice we only have a tag for chests but not potions. This is because the tag will be needed for interactions between the player and chest but the player will not be interacting with the potion besides collison detection.

Under the region `Healthpack_variables`, create a variable with type `GameObject` and name it `healthPotion`. Make sure it is public. We will use this reference to spawn health packs when chests are opened. 

When a player interacts with a chest, the chest should disappear, leaving behind a health potion for the player to pick up. 

**Task 6.2: Implement`DestroyChest()` which destroys a chest and leaves in-place a Health Potion.** 

Functions to modify:

*Chest.cs* -> `DestroyChest()`

Solution (translate hex to ASCII):
```
68 74 74 70 73 3A 2F 2F 79 6F 75 74 75 2E 62 65 2F 50 6C 77 31 4F 30 55 75 5F 7A 51 3F 73 69 3D 51 6B 57 44 64 42 45 6B 6D 47 41 52 53 64 65 62 26 74 3D 34 35 35
```

Back in the Unity editor, with *Chest* selected, drag and drop a reference to the `HealthPotion` prefab into this variable via the Unity inspector. Then, make your `Chest` into a prefab. 

{: .note}
>You won't be able to test your implemention until you've finished the next task.

##  Interacting with Pickups

We just implemented the `Open()` function for *Chest*, that when called, destroys the *Chest* game object and leaves in its place a *Health Potion*. 
As of right now, we can't interact and open the chest. Let's implement that functionality in this section.

The `Open()` function should be called whenever the player presses "E" on a chest.  

First, open up the *PlayerController.cs* script and add a conditional `if statement` inside the `Update()` function to repeatedly check if the player presses the "E" key. If the "E" key is pressed, call the *PlayerController*'s `Interact()` function; we shall implement the functionality of this function in the next step.

```
/* PlayerController.cs */

void Update() {
    if (Input.GetKeyDown(KeyCode.E)) {
        Interact();
    }
}

```

Still inside the *PlayerController.cs* script, navigate down to the Interact() function. This function, when invoked, will check if the player is facing a chest, if so, it will call that particular *Chest* instance's `Open()` function to drop a *Health Potion*.

**Task 6.3: Implement `Interact()`: use a `BoxCastAll` to check if the player is facing a `Chest` game object if so, call that `Chest`'s `Open()` function.**

Functions to modify:

*PlayerController.cs* -> `Interact()`

{: .important}
>`BoxCastAll()` works the same as `CircleCastAll()` but raycasts in the shape of a rectangle instead of a circle. We highly reccommend reading over the documentation here: https://docs.unity3d.com/ScriptReference/Physics.BoxCastAll.html.
For the size parameter we used 0.5f for both its width and height. Keep in mind we want to cast in the direction the player is facing. 

Solution (translate hex to ascii):
```
68 74 74 70 73 3A 2F 2F 79 6F 75 74 75 2E 62 65 2F 4E 74 4F 54 70 67 44 4F 7A 49 30 3F 73 69 3D 52 44 43 64 6F 46 35 74 36 68 6A 77 39 44 30 4A 26 74 3D 37 31
```

Now, scatter some chests into your map by dragging and dropping the `Chest` prefab into your scene multiple times.

![](./images/fig6.3.png) Fig 6.3

Here is a example of what your scene should look like now.

Now you should be able to walk up to the chests, press E for a health potion, and walk over the potion to gain health.
