## Section 6 - Pickups

### Setting up the chest and health-pack
Right click in the hierarchy to create a new sprite game object `2D Object > Sprite` and rename it to `Chest`. Then, follow these steps: 

1. In your project's directory, navigate to `Assets > Sprites > Items` and drag the *Chest.png* into the `Sprite Renderer` component's `Sprite` box.

2. Inside the`Sprite Renderer` component, look under "Additional Settings", set the `Sorting layer` to `Enemy`.

![](./images/fig6.1.png) Fig 6.1

2. Add a `Rigidbody 2D` component and a `Box Collider 2D` component. Change the `Rigidbody 2D`'s body type to `Kinematic`. Kinematic means this game object is unaffected by gravity and can only be moved by scripts.

![](./images/fig6.2.png) Fig 6.2

Now, create another new game object and name it `HealthPack`. Repeat the following steps above for `HealthPack`.

### Healthpack Script

Navigate to the Scripts folder `Assets > Scripts` and open `HealthPack.cs`.

In `HealthPack.cs`, start by creating a new region `HealthPack_variables` and add a int variable named `healthAmount`.

**Task: In `HealthPack.cs` fill in the `OnTriggerEnter2D()` function so the player gains `healAmount` of health when collided with (remember to attach the script to the healthpack game object before testing).**

// add destroy game object

Solution (translate hex to ASCII):
```
68 74 74 70 73 3A 2F 2F 79 6F 75 74 75 2E 62 65 2F 50 6C 77 31 4F 30 55 75 5F 7A 51 3F 73 69 3D 66 74 31 61 6D 35 71 64 4F 6C 6E 77 58 37 70 52 26 74 3D 32 37 39
```

Add your finished script as a component to your HealthPack game object.
Make your `HealthPack` game object into a prefab.

### Chest Script

Navigate to the Scripts folder again and open `Chest.cs`

Under a new region `Healthpack_variables`, create a variable with type `GameObject` and name it `healthpack`. We will need this variable to spawn healthpacks when chests are opened. Back in the unity editor, with `Chest` selected, drag and drop a reference to the `HealthPack` prefab into this variable via the unity inspector.

**Task: fill out the `DestroyChest()` function so a chest is destroyed and leaves in-place a healthpack (Again, make sure to attach the script before testing)** 

Solution (translate hex to ASCII):
```
68 74 74 70 73 3A 2F 2F 79 6F 75 74 75 2E 62 65 2F 50 6C 77 31 4F 30 55 75 5F 7A 51 3F 73 69 3D 51 6B 57 44 64 42 45 6B 6D 47 41 52 53 64 65 62 26 74 3D 34 35 35
```

Add your finished script as a component to your `Chest` game object. Drag and drop a reference to your *HealthPack* prefab into the `Chest` script component.
Make your `Chest` into a prefab. 

Now, scatter some chests into your map by dragging and dropping the `Chest` prefabs into your scene.

![](./images/fig6.3.png) 

Here is a example of what your scene should look like now.
