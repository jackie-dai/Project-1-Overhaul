## Section 6 - Pickups

### Setting up the chest and health-pack
Create a new game object and name it `Chest`. Then, follow these steps: 

1. In the`Sprite Renderer` component and under `Additional Settings`, set the `Sorting layer` to `Enemy`.

2. Add a `Rigidbody 2D` component and a `Box Collider 2D` component. Change the `Rigidbody 2D`'s body type to `Kinematic`.

Now, create another new game object and name it `HealthPack`. Repeat the following steps above for `HealthPack`.

### Healthpack Script

Navigate to the Scripts folder `Assets > Scripts` and open `HealthPack.cs`.

In `HealthPack.cs`, start by creating a new region `HealthPack_variables` and add a int variable named `healthAmount`.

**Task: In `HealthPack.cs` fill in the `OnTriggerEnter2D()` function so the player gains `healAmount` of health when collided with (remember to attach the script to the healthpack game object before testing).**

Make your `HealthPack` game object into a prefab.

### Chest Script

Navigate to the Scripts folder again and open `Chest.cs`

Under a new region `Healthpack_variables`, create a variable with type `GameObject` and name it `healthpack`. We will need this variable to spawn healthpacks when chests are opened. Back in the unity editor, with `Chest` selected, drag and drop a reference to the `HealthPack` prefab into this variable via the unity inspector.

**Task: fill out the `DestroyChest()` function so a chest is destroyed and leaves in-place a healthpack (Again, make sure to attach the script before testing)** 

Drag and drop your working chests into the locations of your choosing.
