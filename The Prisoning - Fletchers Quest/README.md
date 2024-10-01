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

> [!NOTE]
> An example of this can be that the screen eating Beetle would need to do all the normal disabling and resetting when the player dies or leaves the room, but it would also need to tell the "screen eater" script to reset the camera so the player could see normally again.
<img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/beetle.gif" width="400"/> <br>

While the enemies in this game look visually distinct from each other, their movement and attack behaviors are built using modular scripts. This allowed me to reuse scripts with slight tweaks. All enemies would use a "passive attack" script to damage the player on contact, this script only needed to be placed on the prefab where the relevant collider was located and would work with the disabling and enabling functions seamlessly. A "ranged attack" script could also be added to give an enemy the possibility to shoot. This script could easily be tweaked to change shooting cooldown or which projectile prefab to use and add to it's object pool. Movement was built similarly, with 3 base movement types: patrolling, fixed or AIPath. 

<img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/camelSnake.gif" width="400"/>
<img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/twiggyDeaths.gif" width="400"/> 
<img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/sharkLasers.gif" width="400"/> 
<img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/mustang.gif" width="400"/> 
<img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/monkeys.gif" width="400"/> 
<img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/manyGnomes.gif" width="400"/> 
<img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/hamsters.gif" width="400"/> 
<img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/droid.gif" width="400"/> 



### Bosses
<img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/AloneShark.gif" width="400"/> 
<img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/GoldenPirog.gif" width="400"/> 
<img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/Christine.gif" width="400"/> 



### Cutscenes & Dialogue

<img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/dialogue.gif" width="400"/> 
<img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/poster.gif" width="400"/> 
<img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/toilet.gif" width="400"/> 



### Sequence Breaks
<img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/ufo.gif" width="400">
<img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/submarine.gif" width="400">
<img src="https://github.com/MikaelahJ/Portfolio/blob/main/The%20Prisoning%20-%20Fletchers%20Quest/Visuals/karaoke.gif" width="400">




