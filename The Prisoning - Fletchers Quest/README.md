# The Prisoning: Fletcher's Quest

<img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/header.jpg" width=75%>

> After a visit to the psychologist that went horribly wrong you’re trapped in the mind of a game developer on the brink of physical and emotional burnout during the last stages of an intense project. Experience a metroidvania drenched in anxiety based on a very true story.
Help Fletcher Howie Jr. escape his mental prison and save the day!

[Steam page](https://store.steampowered.com/app/2725470/The_Prisoning_Fletchers_Quest/)

## Brief project background
For 6 months, I worked as an intern at Elden Pixels in Gothenburg. I was involved from the start on _The Prisoning: Fletcher's Quest_, a new project in Unity where I had significant responsibility for developing enemies and bosses. During this internship, I created around 20 enemies and 3 bosses from scratch, which was a super fun challenge to program. In addition to working on enemies, I spent a lot of time developing both in-depth systems and various gameplay systems related to enemies and bosses, as well as unique sequence breaks and cutscenes to give the game its distinctive feel.
Currently, I don’t know the release date, but there may be an opportunity to test a demo if you're interested. :)

## My contributions as a programming intern at Elden Pixels

> While the code I've written is secret, the game is not. I'm allowed to show everything I've done and will try my best to explain the systems I've built for this project. Please be aware that this is an early alpha and while some features are polished and complete others may not be :)

### Enemies

One of my main responabilities were the enemy behaviors and animation controllers. Every enemy is pooled in an objectpool to reuse as a new room loads. This meant all enemies need to be able to reset correctly when a room is loaded. All enemies inherit from the same abstract base class which handled essential functionality such as enabling and disabling on room load/unload, taking damage, doing damage and lastly death. 
I would then, where needed, override these core functions for enemies that would need unique behaviors. 

> An example of this is the screen eating Beetle that needed to do all the default disabling and resetting when the player dies or leaves the room, but it would also need to tell the "screen eater" script to reset the camera so the player could see normally again. </br>
> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/beetle.gif" width="400"/> <br>

While the enemies in this game look visually distinct from each other, their movement and attack behaviors are built using modular scripts. This allowed me to reuse scripts with slight tweaks. All enemies would use a "Passive" attack script to damage the player on contact, this script only needed to be placed on the prefab where the relevant collider was located and would work with the disabling and enabling functions seamlessly. A "Ranged" attack script could also be added to give an enemy ranged functionality. This script could easily be tweaked to change shooting cooldown or which projectile prefab to use and add to it's object pool. Movement was built similarly, with 3 base movement types: Patrolling, Fixed or AIPath. 

> This Jetbrain enemy (left) is using the default "Patrolling" movement script with the base "Passive" attack while the hamster enemy (right) uses the same scripts only that it overrides the "turn" function of patrolling movement to rotate it instead of turning. </br>
> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/jetbrain.gif" width="400"/> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/hamsters.gif" width="400"/>

> These enemies both use the "AIPath" movement with the exception that the Mustang (left) only runs it's "Move" function once to place the roads while the Mimic (right) runs repetably to continue following the player. </br>
> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/mustang.gif" width="400"/> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/camelSnake.gif" width="400"/> </br>

Projectiles were setup in a simmilar way, each inheriting from an abstract base projectile class. This class handled enabling/disabling the same way enemies did and checked if out of bounds or when hitting the player. 

> This GnomeDoor is checking if the player is in range before shooting out Gnomes using the "Ranged" script. The Gnomes themselves didn't need any advanced movement and are functionally only a projectile not an enemy. (this is just from removing a spawn time limit for a fun gif) </br>
> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/manyGnomes.gif" width="400"/> </br>

Projectiles could either use a fixed vector direction or some unique behavior by using gravity or following the player.

> These all use the same projectile base with some tweaks. </br>
> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/monkeys.gif" width="400"/> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/droid.gif" width="400"/> </br>

> These lasers the Sharks are screaming were fun to make. I used sprite masks to simulate the laser moving forward at the start of the attack and it disappearing because it is just a long image without animations. There was a lot of tweaking of timings to match animations and collision correctly. </br>
> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/sharkLasers.gif" width="400"/></br>

> And Lastly, what I think is my favorite enemy, poor Twiggy and their family. </br>
> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/twiggyDeaths.gif" width="400"/> </br>



### Bosses
Similarly to the enemies, the bosses also have a base "boss class". This handled the logic around spawning conditions, disabling the player, starting dialogue and closing enviorment doors to set the arena. The bosses run using state machines controlling what to do when switching state and which functions to run in each state. This allowed them to smoothly switch between states and it was easy to see when they switched in editor which helped greatly during testing as i could easily test each state by connecting a debug button. They could also make use of the previously discussed attack and movement scripts which allowed me to quickly make a prototype for the level and game designers to look at and decide which direction the boss should take and specify how the attacks should function. This also made it easier for the artists to decide which animations would be needed.

> Both of these use the "Ranged" script and they either use movement scripts previously used in enemies or use movement scripts i could later implement in other enemies. For the Aloneshark (left) i discovered [bezier curves](https://en.wikipedia.org/wiki/B%C3%A9zier_curve) which i loved playing around with and later used for the Con enemy which we sadly didn't have time to implement fully into the game. </br>
> <sup> As a sidenote this movement would be perfect for a frog enemy. </sup> </br>
> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/AloneShark.gif" width="400"/> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/GoldenPirog.gif" width="400"/> </br>

> For the starting cutscene this boss uses a modified Hamster patroll movement to spawn its healthbar moving along the edge of the screen. It also uses the "Ranged" attack script to throw its tires. </br>
> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/Christine.gif" width="400"/> </br>

### Cutscenes & Dialogue

<img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/dialogue.gif" width="400"/> </br>
<img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/poster.gif" width="400"/> </br>
<img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/toilet.gif" width="400"/> </br>



### Sequence Breaks
<img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/ufo.gif" width="400"> </br>
<img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/submarine.gif" width="400"> </br>
<img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/karaoke.gif" width="400"> </br>




