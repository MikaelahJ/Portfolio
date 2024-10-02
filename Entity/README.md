
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

My main responsability was developing and maintaining the networking part together with another programmer. This was a pretty big challenge as neither of us had tried multiplayer in Unreal Engine but it turned out to be both a buggy and fun experience. My favorite bug was when the host could kill all clients no problem, but if the clients tried to kill the host they would instantly die themselves. A client shooting another client resulted in both dying :) <br>
This was of course fixed as we dove deeper into the networking nest of Unreal. <br>

<img src="https://github.com/MikaelahJ/Portfolio/blob/main/Entity/Visuals/hostGame.gif" width="400"> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/Entity/Visuals/playersInLobby.gif" width="400"> <br>

<details>
  <summary> Spawning a death box </summary> <br>
  <img src="https://github.com/MikaelahJ/Portfolio/blob/main/Entity/Visuals/deathbox.png" width=100%> <br>
</details>


### VFX, Niagara
I developed the system for all of the weapon VFX using Niagara with assets from our artists and by tweaking finished assets from the Epic Marketplace.
> This is an older gif where animations were not yet hooked up.
> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/Entity/Visuals/weaponFX1.gif" width="400"> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/Entity/Visuals/weaponFX2.gif" width="400"> <br>

<details>
  <summary> Weapon VFX Blueprint </summary> <br>
  <img src="https://github.com/MikaelahJ/Portfolio/blob/main/Entity/Visuals/weaponFX0.png" width=100%> <br>
  <img src="https://github.com/MikaelahJ/Portfolio/blob/main/Entity/Visuals/weaponFX1.png" width=100%> <br>
  <img src="https://github.com/MikaelahJ/Portfolio/blob/main/Entity/Visuals/weaponFX2.png" width=100%> <br>
</details>


### Death Boxes
When a player dies they drop what we called a "Death Box". This is where their items and pickups were stored for other players to loot. I made these by saving all of the players items and then when spawning the box just add the types of items and how much ammo each weapon had. I also setup the UI for these and made sure it clearly showed what was inside. 

<img src="https://github.com/MikaelahJ/Portfolio/blob/main/Entity/Visuals/deathbox.gif" width="400"> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/Entity/Visuals/deathboxUI.gif" width="400"> <br>

<details>
  <summary> Spawning a death box </summary> <br>
  <img src="https://github.com/MikaelahJ/Portfolio/blob/main/Entity/Visuals/deathbox.png" width=100%> <br>
</details>

<details>
  <summary> Death box UI </summary> <br>
  <img src="https://github.com/MikaelahJ/Portfolio/blob/main/Entity/Visuals/deathboxUI.png" width=100%> <br>
</details>


### Some fun commits to end this page :)
  <img src="https://github.com/MikaelahJ/Portfolio/blob/main/Entity/Visuals/gitCommits.png" width=100%>
