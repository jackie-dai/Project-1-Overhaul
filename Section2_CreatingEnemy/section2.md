## Section 2

What fun is a game if there are no enemies to fight?

In this section, we will be creating a enemy for the player to fight. The enemy will have a line of sight and if the player is within the enemy's line of sight, it will move towards the player and explode upon contact; dealing damage to the player. In return, the player will also be able to deal damage back to the enemy. 

Like you did with the player, make a new game object and name it *Enemy*, but this time attach a Circle Collider 2D. 
Modify the Rigidbody 2D by:

- setting gravity to zero
- freezing z rotation

Like so:
[insert fig1]

Next, set the Enemy game object's tag to Enemy.
Now, we have a basic enemy game object. 

An enemy should attack the player if the player is within a certain radius. 

To create a detection system, lets make a new game object that is a **child of the Enemy game object**; name this game object *LineOfSight*. Attach a Circle Collider 2D to the *LineOfSight* game object and **check the IsTrigger checkbox**. When the player game object is within this circle collider, this will tell the enemy to move and attack the player; adjust the radius of the LineOfSight collider to fit your desired range. We are going to go with 4. 

[insert img of LineOfSight Inspector]

Now, we need to implement the logic to make the enemy move towards and attack the player. 
Make a new script in the scripts folder and name it *Enemy*. Inside the *Enemy* script, set up 3 regions:

1. Movement_variables
2. Unity_functions
3. Movement_functions


![](./images/fig3.png)
[insert image of the three regions --fig3]