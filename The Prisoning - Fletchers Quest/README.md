# The Prisoning: Fletcher's Quest

<img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/header.jpg" width=75%>

> After a visit to the psychologist that went horribly wrong you’re trapped in the mind of a game developer on the brink of physical and emotional burnout during the last stages of an intense project. Experience a metroidvania drenched in anxiety based on a very true story.
Help Fletcher Howie Jr. escape his mental prison and save the day!

[Steam page](https://store.steampowered.com/app/2725470/The_Prisoning_Fletchers_Quest/)

## Brief project background
For 6 months, I worked as an intern at Elden Pixels in Gothenburg. I was involved from the start on _The Prisoning: Fletcher's Quest_, a new project in Unity where I had significant responsibility for developing enemies and bosses. During this internship, I created around 20 enemies and 3 bosses from scratch, which was a super fun challenge to program. In addition to working on enemies, I spent a lot of time developing both in-depth systems and various gameplay systems related to enemies and bosses, as well as unique sequence breaks and cutscenes to give the game its distinctive feel.
Currently, I don’t know the release date, but there may be an opportunity to test a demo if you're interested. :)

## My contributions as a programming intern at Elden Pixels
>[!NOTE]
> While the code I've written is secret, the game is not. I'm allowed to show everything I've done and will try my best to explain the systems I've built for this project. Please be aware that this is an early alpha and while some features are polished and complete others may not be. I also apologize in advance for the quality of some of the following gifs :)

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

Projectiles were setup in a similar way, each inheriting from an abstract base projectile class. This class handled enabling/disabling the same way enemies did and checked if out of bounds or when hitting the player. 

> This GnomeDoor is checking if the player is in sight before shooting out Gnomes using the "Ranged" script. The Gnomes themselves didn't need any advanced movement and are functionally only a projectile not an enemy. (this endless stream is just from removing a spawn time limit for a fun gif) </br>
> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/manyGnomes.gif" width="400"/> </br>

Projectiles could either use a fixed vector direction or some unique behavior by using gravity or following the player.

> These all use the same projectile base with some tweaks to speed, gravity or directions. </br>
> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/monkeys.gif" width="400"/> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/satanist.gif" width="400"/> </br>
> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/screamer.gif" width="400"/> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/droid.gif" width="400"/> </br>

> These lasers the Sharks are screaming were fun to make. I used sprite masks to simulate the laser moving forward at the start of the attack and it disappearing because it is just a long image without animations. There was a lot of tweaking of timings to match animations and collision correctly. </br>
> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/sharkLasers.gif" width="400"/></br>

> And Lastly, what I think is my favorite enemy, poor Twiggy and their family. </br>
> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/twiggyDeaths.gif" width="400"/> </br>


### Bosses
Similarly to the enemies, the bosses also have an abstract base boss class. This handled the logic around spawning conditions, disabling the player, starting dialogue and closing enviorment doors to set the arena. The bosses run using state machines controlling what to do when switching state and which functions to run in each state. This allowed them to smoothly switch between states and it was easy to see when they switched in editor which helped greatly during testing as i could easily test each state by connecting debug buttons. They could also make use of the previously discussed attack and movement scripts which allowed me to quickly make a prototype for the level and game designers to look at and decide which direction the boss should take and specify how the movement and attacks should function. This also made it easier for the artists to decide which animations would be needed.

> Both of these use the "Ranged" script and they either use movement scripts previously used in enemies or use movement scripts i could later implement in other enemies. For the Aloneshark (left) i discovered [bezier curves](https://en.wikipedia.org/wiki/B%C3%A9zier_curve) which i loved playing around with and later used for the Con enemy which we sadly didn't have time to implement fully into the game. </br>
> <sup> As a sidenote this movement would be perfect for a frog enemy. </sup> </br>
> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/AloneShark.gif" width="400"/> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/GoldenPirog.gif" width="400"/> </br>

> For the starting cutscene this boss uses a slightly modified Hamster patroll movement to spawn its healthbar moving along the edge of the screen. It also uses the "Ranged" attack script to throw its tires. </br>
> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/christine.gif" width="400"/> </br>
<!-- add gif of healthbar spawning -->


### Cutscenes & Dialogue
I also created a bunch of cutscenes using Unity's Timeline asset and systems to play correct dialogue based on how far the player has gotten or what the player has collected. Timelines require a lot of tweaking to get perfect timings which would take some time but it was also very satisfying and fun to sit with. 

<img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/dialogue.gif" width="400"/> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/poster.gif" width="400"/></br>
<img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/toilet.gif" width="400"/> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/collection.gif" width="400"/>


### Sequence Breaks
These were some of the most fun to make and play around with. I developed everything from the movement types of the submarine and UFO to the cutscenes and level loading surrounding them to the enemies and obstacles. </br>

> For the UFO sequence I made scriptable objects to save the different waves that were to spawn. My wave spawner script would then load these and run through them until they were finished. This made it easy to playtest and add, remove or change variables of specific 
> waves. The scriptable objects would save what prefab to spawn, in what pattern they would spawn, spawn delays and time to wait until next wave. </br>
> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/ufo.gif" width="400">

> We needed a water shader for this submarine sequence so I got the chance to dive into both shader code and shader graphs for the first time. This was both very fun and very frustrating. There were many problems with it only working on specific layers or it just being way to much and making the level disorienting. </br>
> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/submarine.gif" width="400"> </br>

> This karaoke sequence was made using a timeline sending signals during the audiotrack of the song playing to tell my platform spawner script to spawn a new platform with the next line from the lyrics. This was a fan favorite of playtesters who thought it was very funny :) </br>
> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/karaoke.gif" width="400"> 

### Not included in demo at the time I was there 
There were some things that i developed and put a lot of effort and time into but we just didn't have the time to fully design and implement them. </br>

> We wanted to add these "anxiety blobs" as a sort of currency and to support the story of Fletcher removing the anxiety from his mind. I made a fully working system for saving the currency and adding when destroying the anxiety. This currency would be used in a shop to   gain upgrades but we later chose to give the player upgrades after defeating bosses instead. I also made this "wobble" shader for the anxiety to make them seem less static and more alive. </br>
> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/wobbleShader.gif" width="400"> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/upgradesShop.gif" width="400"> </br>

> There were also plans for a smarter enemy. I made my own AI for this enemy using raycasts to figure out where they could jump to based on tweakable variables determining how high or long jumps they could do. This was super fun to test and fix all the cases where it would jump though tiles or getting stuck in corners. I made 2 states for this enemy where it in the "hunting" state would try to get to the players level to shoot them and a "hiding" state which it would enter if it got hurt. In the hiding state it would try to get as far away from the player it could to "regroup" for a second before switching into hunting mode again. </br>
> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/aiEnemy.gif" width="400"> </br>

### Some fun gifs to end this page :)
<img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/horseDance.gif" width="400"> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/flyingCon.gif" width="400"> </br> 
<img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/messyShader.gif" width="400"> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/wrongSprite.gif" width="400"> </br> 
<img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/slamDoor.gif" width="75%"> 
