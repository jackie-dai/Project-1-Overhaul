## Section 3 - Health and Damage

In this game, the player and the enemy want to take the other down in glorious combat. But without both health and damage systems, neither side can do anything to the other. 

Our goal for this section is to allow the player and enemy to defeat each other during the game as they exchange successful attacks.

## Health System

#### Summary:
1. Update the PlayerController and Enemy scripts to store health and damage for both enemies and players.
2. Send damage values from the players to the enemies when an attack lands, and vice versa.

Open the `PlayerController` script and take a look under the region called `Health_variables`.

```
#region Health_variables
public float maxHealth = 5;
float currHealth = 5;
#endregion
```

- `currHealth` holds the player's current amount of health.
- `maxHealth` holds the maximum amount of health that the player can hold at one time.

Now, scroll down to the `Health_functions` region, where three functions have been set up for you. These functions are responsible for changing the player’s health as the player either takes damage or heals damage. You will be implementing two of these functions.

```   
#region Health_Functions
//take damage based on value param passed in by caller
public void TakeDamage(float value){
    //TO BE IMPLEMENTED
}
//heal player
public void Heal(float value){
    //TO BE IMPLEMENTED
}
#endregion

//destroy player object and triggers end scene
private void Die(){
    Destroy(this.gameObject);
}
```
**Task 3.1: Implement `TakeDamage()`, and `Heal()` in the PlayerController script. Implement `TakeDamage()`, in the Enemy script.**

1. Using the `value` parameter, change `currHealth` inside of the `TakeDamage()` and `Heal()` functions depending on if the player is receiving damage or healing damage.
    - Call the `Die()` function whenever the player receives too much damage.
    - Limit `currHealth` to `maxHealth` when healing damage, since we do not want `currHealth` to surpass `maxHealth` when implementing the health bar.
    - Add a `Debug.Log()` to `TakeDamage()`, containing a message that displays `currHealth`'s value for debugging purposes.
    - In the `Awake()` function of *PlayerController.cs*, set `currHealth` equal to `maxHealth`. This ensures that the player starts with a full health bar when the game starts.
2. In the `Enemy` script, implement `TakeDamage()` using the same code logic in the `PlayerController` script.

Functions to modify:

*PlayerController.cs* -> `TakeDamage()`, `Heal()`, and `Awake()`

*Enemy.cs* -> `TakeDamage()`


{: .important}
> Below is the hex code for the solution.

```
Solution: 68 74 74 70 73 3A 2F 2F 79 6F 75 74 75 2E 62 65 2F 72 59 4A 52 31 41 34 4B 4F 67 6B 3F 6C 69 73 74 3D 50 4C 6B 54 71 66 35 44 42 7A 50 73 41 65 2D 70 52 35 62 44 55 64 77 48 69 43 4E 67 48 63 79 42 49 68 26 74 3D 31 31 30
```

Now, both the enemy and the player have a functional health system, but they do not have a way to damage one another. To add a damage system, we will be using 2D raycasts.

## Damage System
Head to the `AttackRoutine()` function within the PlayerController script. This function is called whenever the player attacks. Within the foreach loop, the player object is checking whether there are any objects with the Enemy tag inside of the attack hitbox, and returning any objects that it finds.
```    
RaycastHit2D[] hits = Physics2D.BoxCastAll(PlayerRB.position + curr_direction, Vector2.one, 0f, Vector3.zero);

foreach(RaycastHit2D hit in hits){
    Debug.Log(hit.transform.name);
    if (hit.transform.CompareTag("Enemy")){
        Debug.Log("Tons of damage");
        //TO BE IMPLEMENTED
    }
}
    
```

**Task 3.2: Fill in the logic for AttackRoutine() in the PlayerController script and Explode() in the Enemy script.**

1. Using the `transform.CompareTag()` function, call the `TakeDamage()` function inside of the enemy's `Enemy` script.
    - The variable `hit` refers to the GameObject of an enemy within the player’s attack hitbox.
    - This may be a good time to use the `GetComponent<>()` function!
2. In the `Enemy` script, call `TakeDamage()` inside of the player's `PlayerController` script through the `Explode()` function. 
    - Additionally, destroy the enemy GameObject when the enemy hitbox finds its target.
    - Look at the code from PlayerController and take note of how they access variables from GameObjects that are caught in the raycasts.
    - Make sure that you're not using the `Player` transform variable.

Functions to modify:

*PlayerController.cs* -> `AttackRoutine()`

*Enemy.cs* -> `Explode()`

{: .important}
> Below is the hex code for the solution.
```
Solution: 68 74 74 70 73 3A 2F 2F 79 6F 75 74 75 2E 62 65 2F 72 59 4A 52 31 41 34 4B 4F 67 6B 3F 6C 69 73 74 3D 50 4C 6B 54 71 66 35 44 42 7A 50 73 41 65 2D 70 52 35 62 44 55 64 77 48 69 43 4E 67 48 63 79 42 49 68 26 74 3D 35 36 37
```

Now the enemy and player in our game can deal damage and kill each other. Adjust the `maxHealth` value of the player in the inspector to test out if the player takes damage as expected, and they die if, and only if, the player reaches 0 health.
