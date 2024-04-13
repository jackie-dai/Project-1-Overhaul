## Section 5 - Sound and Camera

In this section, you will handle all the sound aspects of the project, along with a couple bits and pieces that we need to pick up before moving on.


## Audio


First, enable the *AudioManager* object in the Hierarchy. Then, in your *Player* script, add the sounds where you want it to be played. In order to do this, you will need to add this line of code to where you want the sound to be played: `FindObjectOfType<AudioManager>().Play("SoundName");`. 

To find the names of each sound, go into the *AudioManager* object, and click on each sound dropdown to find the *Name* field. You will need to add this line for each sound in their respective locations. The link to the tutorial with the timestamp can be found below.

**Task 5.1: Implement all sounds listed in the *AudioManager* in their respective places**

Here is a list of the sounds you'll need to implement:

- PlayerHurt
- PlayerDeath
- Explosion
- EnemyHurt
- PlayerAttack
  
{: .hint}
>Make sure to play the sound *before* the object is destroyed, or else it will not play!

{: .important}
>Potions are not yet implemented, so there is no need to add the potion effect. **You will implement the sound for the potion during the next section.**

Solution (translate hex to ASCII):
```
68 74 74 70 73 3A 2F 2F 79 6F 75 74 75 2E 62 65 2F 41 6D 6F 49 5A 34 41 55 75 72 45 3F 6C 69 73 74 3D 50 4C 6B 54 71 66 35 44 42 7A 50 73 41 65 2D 70 52 35 62 44 55 64 77 48 69 43 4E 67 48 63 79 42 49 68 26 74 3D 36 37
```


## Bits and Pieces

Now, we want the camera to move with the player. So, click on the *CM vcam1* object in the Hierarchy, and check it. Then, in the `CinemachineVirtualCamera` component, drag your *Player* object into the Follow area. Then, go into the `Main Camera` and check the `CinemachineBrain` component. You should now be able to play the game with the camera centered on the player, as you explore the map.

In your hierarchy, create an empty `GameObject` called *Enemies*, and drag each Enemy into this empty object. This keeps your Hierarchy clean and organized!

Now, you should be able to play your game in the map, and have sound effects along with it! 
