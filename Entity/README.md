
# ENTITY

<img src="https://github.com/MikaelahJ/Portfolio/blob/main/Entity/Visuals/header.jpg" width=75%>

> In the distant future, humanity is on the verge of extinction. Their new world regime, e-corps are the sole suppliers of food and water, thus the people of earth must obey.
They have set up an inhumane arena, where you plug yourself into their neural engine and fight within the mind of their entity. Pain is real, death is not.
The champion of the game is the only one to win the prize, and the only one who will be able to buy food for the day.

[Itch.io page](https://yrgo-game-creator.itch.io/entity)

## Brief project background
Entity was a 7-week project during the spring of 2023 where my team developed a LAN multiplayer FPS in Unreal Engine 5 (Blueprints) set in a dark environment with various light-related abilities. I, together with another programmer, primarily handled the networking aspect and integrated the other team members' features to function and replicate for all players simultaneously. I also worked extensively on developing our VFX and ensuring they displayed correctly for all players.


## My contributions to this project
### Networking & Replication

One of my main responabilities were the enemy behaviors and animation controllers. Every enemy is pooled in an objectpool to reuse as a new room loads. This meant all enemies need to be able to reset correctly when a room is loaded. All enemies inherit from the same abstract base class which handled essential functionality such as enabling and disabling on room load/unload, taking damage, doing damage and lastly death. 
I would then, where needed, override these core functions for enemies that would need unique behaviors. 

> An example of this is the screen eating Beetle that needed to do all the default disabling and resetting when the player dies or leaves the room, but it would also need to tell the "screen eater" script to reset the camera so the player could see normally again. </br>
> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/beetle.gif" width="400"/> <br>


### VFX, Niagara
I developed the system for all of the weapon VFX using Niagara with assets from our artists and by tweaking finished assets from the Epic Marketplace. 

<img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/AloneShark.gif" width="400"/> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/GoldenPirog.gif" width="400"/> </br>

> Both of these use the "Ranged" script and they either use movement scripts previously used in enemies or use movement scripts i could later implement in other enemies. For the Aloneshark (left) i discovered [bezier curves](https://en.wikipedia.org/wiki/B%C3%A9zier_curve) which i loved playing around with and later used for the Con enemy which we sadly didn't have time to implement fully into the game. </br>
> <sup> As a sidenote this movement would be perfect for a frog enemy. </sup> </br>
> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/AloneShark.gif" width="400"/> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/GoldenPirog.gif" width="400"/> </br>

### Death Boxes
When a player dies they drop what we called a "Death Box". This is where their items and pickups were stored for other players to loot. I made these by saving all of the players items and then when spawning the box just add the types of items and how much ammo each weapon had. I also setup the UI for these and made sure it clearly showed what was inside. 
<details>
  <summary> Click here to show blueprints </summary> <br>
  <img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/dialogue.gif" width="400"/>
  <img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/poster.gif" width="400"/>
</details>
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
