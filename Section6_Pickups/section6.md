## Section 6 - Pickups

### Setting up the chest and health-pack
Create a new game object and name it `Chest`. Then, follow these steps: 

1. In the`Sprite Renderer` component and under `Additional Settings`, set the `Sorting layer` to `Enemy`.

2. Add a `Rigidbody 2D` component and a `Box Collider 2D` component. Change the `Rigidbody 2D`'s body type to `Kinematic`.

Now, create another new game object and name it `HealthPack`. Repeat the following steps above for `HealthPack`.

### Healthpack Script

Create a new script named `Healthpack`