# Employee Of The Month

<img src="https://github.com/MikaelahJ/Portfolio/blob/main/Employee%20Of%20The%20Month/Visuals/fire.gif" width=75%>

> A 2D top down game where you get the chance to take out all your office aggression against your friends in a two- to four person shooter office showdown to become the Employee of the month!

[Itch.io page](https://yrgo-game-creator.itch.io/employee-of-the-month) <br>
[Repository](https://github.com/MikaelahJ/EmployeeOfTheMonth)

## Brief project background
Employee of the Month was created with 7 classmates during a 7-week project course at Yrgo in the winter of 2022-2023. My primary responsibilities were developing weapon upgrades and features, as well as a local co-op lobby where up to 4 players could join, choose characters and start correctly. All upgrades were designed to be combinable and work together, allowing for "ultimate attacks" with specific combinations. Working on this game taught me a great deal about game design, graphics, and the game development process.

## My contributions to this project
I was basically the jack of all trades during this project so the things I've done are all over the place but I've tried to gather my contributions here. This was my first bigger project with a team and I'm very proud of it, that said, there's a lot I've learned since then and the amount of GetComponents and Instatiate without any pooling or optimisation is getting hard to look at :) <br>

Click dropdowns to view the code!

___
### Character Select
I worked a lot with the character select where each player controller needed to connect to it's own coloured cursor and save which character each player choose. This was used to show correct sprites and colours in-game and during both the intermission (Coffee break) screen and the end screen showing the employee of the month (winner). I did this by saving the character to a playername / player ID, both of which were named 1-4. Spawning the player would then get the player ID to set the correct sprite. I also added the countdown UI at the beginning of the match using animators and screenshake in sync with the sounds. <br>

<img src="https://github.com/MikaelahJ/Portfolio/blob/main/Employee%20Of%20The%20Month/Visuals/characterSelect.gif" width="400"> 

>  We got a lot of feedback from playtests that it was hard to keep track of your own player at the start of each map as the spawnpoints randomise the player to a new one each time. Our solution to this was a circle of the players colour around player as well as arrows at the start of the game. <br>
> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/Employee%20Of%20The%20Month/Visuals/spawning.gif" width="400">

<details>
  <summary> Connect selected character to player controller </summary> <br>
  
```C#
public void ConnectCharacterToPlayer(string playerName, string SelectedCharacter)
{
     int selectedCharacter = Convert.ToInt32(SelectedCharacter);
     if (players.ContainsKey(playerName))
         players[playerName] = selectedCharacter;
     else
         players.Add(playerName, selectedCharacter);

     playersChosen = players.Count;
}
```
</details>

<details>
  <summary> Spawn players </summary> <br>

```C#
private void SpawnPlayer()
{
    player = Instantiate(playerPrefab, SpawnManager.instance.GetRandomSpawnPoint(), transform.rotation);
    player.name = "P" + (playerInput.playerIndex + 1).ToString() + " Player";
    playerMovement = player.GetComponent<Movement>();
    aim = player.GetComponent<Aim>();

    SetFlashlightsOnOff();

    //Rumble
    AddRumble();

    player.GetComponent<Movement>().animator = player.GetComponent<Animator>();

    player.GetComponent<HasHealth>().playerIndex = playerInput.playerIndex;
    player.GetComponent<HasHealth>().animator = player.GetComponent<Animator>();

    GameObject circle = Instantiate(playerHighlightCircle, player.transform);
    circle.GetComponent<SpriteRenderer>().color = pColors[playerInput.playerIndex];

    //Show who is who at start of round
    GameObject whichPlayer = Instantiate(whichPlayerArrow, player.transform.position, Quaternion.identity);
    
    //Keep track of leader each round by spawning mug over head
    List<int> playersInlead = GameManager.Instance.CountPoints();

    foreach (int index in playersInlead)
    {
        int playerNumber = index + 1;
        if (player.name == "P" + playerNumber + " Player")
        {
            GameObject leadermug = Instantiate(leaderMugPrefab, new Vector2(player.transform.position.x, player.transform.position.y), Quaternion.identity);
            leadermug.transform.SetParent(player.transform);
        }
    }

    foreach (var sprite in whichPlayer.GetComponentsInChildren<SpriteRenderer>())
    {
        sprite.sprite = cursorSprites[playerInput.playerIndex];
        Destroy(whichPlayer, 0.5f);
    }

    if(playerTeam != null)
    {
        circle.GetComponent<SpriteRenderer>().color = pColors[(int)playerTeam.GetTeamName() - 1];
    }
    player.GetComponent<HasHealth>().team = playerTeam;
}
```
</details>

___
### Point Saving

I also developed the system to save points and then checking them to show accurately during the "Coffee Break" screen at the half time and also the winner portrait at the end. It also checks after the last round if there needs to be a tiebreaker and then spawns only the correct tiebreaker players for a final round. 

> This break is to show the players who's in lead at the middle point of a match as we didn't display the points during the game. It helped to kind of up the stakes and make some players team up against the leader. We later also added a coffee cup over the leaders head at the beginning of a match to be more clear about who exactly is in lead. <br>
> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/Employee%20Of%20The%20Month/Visuals/intermission.gif" width="400"> 


<details>
  <summary> add points and check winner and tiebreaker </summary>

```C#
public void AddPointsToPlayer(string playerName, int points)
{
    if (playerPoints.ContainsKey(playerName))
    {
        playerPoints[playerName] += points;
    }
    else
    {
        playerPoints.Add(playerName, points);
    }
}

public List<int> GetWinner()
{
    List<int> winner = CountPoints();
    return winner;
}

public int GetWinnerSprite(int winner)
{
    int winnerSprite = players["P" + winner.ToString()];
    return winnerSprite;
}

public List<int> CountPoints()
{
    int result = 0;
    List<int> winner = new List<int>(playersCount);

    for (int i = 0; i < playerPoints.Count; i++)
    {
        if (playerPoints["P" + i.ToString()] > result)
        {
            result = playerPoints["P" + i];
            winner.Insert(0, i);
        }
        else if (playerPoints["P" + i.ToString()] == result && playerPoints["P" + i.ToString()] > 0)
        {
            winner.Add(i);
        }
    }
    return winner;
}

public void SetTiebreaker(List<int> winners)
{
    tiebreaker = true;
    GameModeManager.Instance.currentMode = Gamemodes.FreeForAll;
    foreach (int winner in winners)
    {
        tiebreakers.Add(winner);
    }
    SpawnManager spawnManager = GameObject.Find("SpawnPoints").gameObject.GetComponent<SpawnManager>();
    spawnManager.RestartMatch();
}

public void StartTiebreaker()
{
    if (GameObject.FindGameObjectWithTag("GameOverCanvas") != null)
    {
        playSceneCanvas = GameObject.FindGameObjectWithTag("GameOverCanvas").GetComponent<Canvas>();
        playSceneCanvasTextImage = playSceneCanvas.GetComponentInChildren<Image>();
    }
    StartCoroutine(TiebreakerText());
}
```
</details>

___
### Weapon Modifiers

Some of the more enjoyable systems I worked on were the weapon modifiers, these were both fun to develop and test as different combinations could leed to some fun moments during development. I developed some of the "Ultimate" combination attacks that activate when getting 3 of the same modifier. The greatest example of this is the super microwave which shoots a laser, with a lot of damage but very slow rotation speed, for a couple seconds. This was made using a line renderer with a small shader and particle systems. <br>

<img src="https://github.com/MikaelahJ/Portfolio/blob/main/Employee%20Of%20The%20Month/Visuals/modifiers.png" width="400"> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/Employee%20Of%20The%20Month/Visuals/modifyWeapons.gif" width="400"> <br>
<img src="https://github.com/MikaelahJ/Portfolio/blob/main/Employee%20Of%20The%20Month/Visuals/mikroLaser.gif" width="400"> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/Employee%20Of%20The%20Month/Visuals/Shotgun.gif" width="400">

<details>
  <summary> Microwave Exploding Shots </summary>

``` C#
private void Explode(Vector2 collisionPoint, Collision2D collision)
{
    if (hasExploded) { return; }
    hasExploded = true;

    var explosion = Instantiate(explosionPrefab, transform.position, transform.rotation);
    explosion.transform.localScale = new Vector3(explodeRadius, explodeRadius, explodeRadius);
    Destroy(explosion, 1.5f);

    Collider2D[] targetsInRadius = Physics2D.OverlapCircleAll(collisionPoint, explodeRadius);

    foreach (var target in targetsInRadius)
    {
        SendDamage(explosionDamage, target, collision);
    }
}
```
</details>

<details>
<summary> Ultimate Shotgun Modifyer </summary>

  ```C#
private void FireShotgun()
{
    float startOffset = shotgunAmount / 2 * shotgunSpreadBetween;

    for (int i = 0; i < shotgunAmount; i++)
    {
        GameObject newBullet = Instantiate(bulletPrefab, firePoint.position, transform.rotation);
        newBullet.GetComponent<Bullet>().UpdateBulletModifyers(weaponController.weapon);
        newBullet.GetComponent<Bullet>().bulletOwner = ownerCollider;
        newBullet.transform.Rotate(new Vector3(0, 0, -startOffset + i * 5));
    }

    //Play shotgun fire animation
    fireAnimation.SetTrigger("fireShotgun");
    LoseAmmo();
}
```
</details>

<details>
  <summary> Microwave Laser </summary>

``` C#
using System;
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Laser : MonoBehaviour
{
    [SerializeField] Transform superMicroPos;
    [SerializeField] GameObject superMicro;
    [SerializeField] GameObject superMicroPull;

    private Aim aim;
    private Movement movement;
    private Fire fire;

    public LineRenderer lineRenderer;
    public Transform firePoint;

    public GameObject startVFX;
    public GameObject endVFX;
    private float damage = 100;
    public bool isCharged = false;
    public bool isCharging = false;
    public bool isShooting = false;
    private bool hasStarted = false;
    private bool isDiscarded = false;

    private float defaultWalkSpeed;

    [SerializeField] private LayerMask ignore;

    private Quaternion rotation;
    private List<ParticleSystem> particles = new List<ParticleSystem>();

    void Start()
    {
        hasStarted = true;
        aim = GetComponentInParent<Aim>();
        movement = GetComponentInParent<Movement>();
        fire = GetComponentInParent<Fire>();
        FillLists();
        StartCoroutine(DisableLaser());
    }

    void Update()
    {
        RotateToAim();
        UpdateLaser();
    }

    public void PowerUpLaser()
    {
        isDiscarded = false;
        isCharging = true;
        if (superMicroPos.childCount == 0)
        {
            var superMicroSprite = Instantiate(superMicro, superMicroPos);
            var superMicroSpritePull = Instantiate(superMicroPull, superMicroPos);
        }
        superMicroPos.GetChild(1).GetComponent<Animator>().SetTrigger("Charging");
        superMicroPos.GetChild(0).GetComponent<Animator>().SetTrigger("Charging");

        Invoke(nameof(SetCharged), 1);
    }

    private void SetCharged()
    {
        isCharging = false;
        if (!isDiscarded) {
            isCharged = true;
        }
    }

    public void FireLaser()
    {
        isShooting = true;

        if (aim == null)
            aim = GetComponentInParent<Aim>();
        aim.rotationSpeed = 0.9f;

        EnableLaser();
        UpdateLaser();
        StartCoroutine(DisableLaser());
    }

    public void EnableLaser()
    {
        lineRenderer.enabled = true;
        Camera.main.GetComponent<ScreenShakeBehavior>().TriggerShake(3, 0.07f);

        if (movement == null)
            movement = GetComponentInParent<Movement>();

        defaultWalkSpeed = movement.walkSpeed;
        movement.walkSpeed *= 0.1f;

        for (int i = 0; i < particles.Count; i++)
            particles[i].Play();
    }

    public void UpdateLaser()
    {
        RaycastHit2D hit = Physics2D.Raycast(transform.position, firePoint.transform.up, 20, ~ignore);//send raycast and ignore modifyers
        if (hit)
        {
            SendDamage(hit.collider, damage * Time.deltaTime * 2.5f);
            lineRenderer.SetPosition(1, hit.point);
        }

        lineRenderer.SetPosition(0, (Vector2)firePoint.position);
        startVFX.transform.position = (Vector2)firePoint.position;

        endVFX.transform.position = lineRenderer.GetPosition(1);
    }

    private void SendDamage(Collider2D collider, float damage)
    {
        if (collider.gameObject.transform.CompareTag("Player"))
        {
            if (collider.transform.parent.transform.TryGetComponent<HasHealth>(out HasHealth health))
            {
                health.LoseHealth(damage);
            }
        }

        if (collider.transform.GetComponent<HasHealth>() != null)
        {
            collider.transform.GetComponent<HasHealth>().LoseHealth(damage);
        }
        if (collider.gameObject.GetComponent<ItemBreak>() != null)
        {
            collider.gameObject.GetComponent<ItemBreak>().TakeDamage(damage);
        }
    }

    IEnumerator DisableLaser()
    {
        yield return new WaitForSeconds(3);
        if (!isDiscarded)
        {
            superMicroPos.GetChild(0).GetComponent<Animator>().SetTrigger("Fired");

            ResetLaser();

            fire.DeActivateLaser();
        }
    }

    private void ResetLaser()
    {
        isShooting = false;
        isCharged = false;
        isCharging = false;
        lineRenderer.enabled = false;
        aim.rotationSpeed = 30;
        movement.walkSpeed = defaultWalkSpeed;

        fire.DeActivateLaser();

        for (int i = 0; i < particles.Count; i++)
            particles[i].Stop();
    }

    void RotateToAim()
    {
        Vector2 aimDirection;
        if (aim.hasGamePad)
        {
            aimDirection = aim.aimDirection - (Vector2)transform.position;
        }
        else
        {
            aimDirection = aim.mousePosition - transform.position;
        }

        float angle = Mathf.Atan2(aimDirection.y, aimDirection.x) * Mathf.Rad2Deg;
        rotation.eulerAngles = new Vector3(0, 0, angle);
        transform.rotation = rotation;
    }

    void FillLists()
    {
        for (int i = 0; i < startVFX.transform.childCount; i++)
        {
            var ps = startVFX.transform.GetChild(i).GetComponent<ParticleSystem>();
            if (ps != null)
                particles.Add(ps);
        }

        for (int i = 0; i < endVFX.transform.childCount; i++)
        {
            var ps = endVFX.transform.GetChild(i).GetComponent<ParticleSystem>();
            if (ps != null)
                particles.Add(ps);
        }
    }

    public void DiscardSuperSprite()
    {
        isDiscarded = true;

        if (superMicroPos.childCount == 0)
        {
            return;
        }
        superMicroPos.GetChild(0).GetComponent<Animator>().Play("LaserDefault");
        superMicroPos.GetChild(1).GetComponent<Animator>().Play("LaserDefaultPull");
        GetComponentInParent<Fire>().FadeLaserSound();
        if (hasStarted) 
        {
            ResetLaser();
        }
    }
}
```
</details>

___
### Maps, Lightning & Breakables

I was responsable for implementing the artists vision of how the maps should look with both breakable furniture / items and lightning. We also decided to create a night version of each map to double the maps and add more variety. Since I already made the other map scenes I also made these night versions, adding lights with the help of an artist as well as a flashlight for the players. <br>

<img src="https://github.com/MikaelahJ/Portfolio/blob/main/Employee%20Of%20The%20Month/Visuals/destruction.gif" width="400"> <img src="https://github.com/MikaelahJ/Portfolio/blob/main/Employee%20Of%20The%20Month/Visuals/nightMap.gif" width="400">

<details>
  <summary> Item Break </summary>

```C#
using System;
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class ItemBreak : MonoBehaviour
{
    [Header("Sprites in order first to last")]
    [SerializeField] private List<Sprite> spritesBeforeBreak = new List<Sprite>();
    [SerializeField] private Animator animator;
    [SerializeField] private SpriteRenderer spriteRenderer;
    [SerializeField] private GameObject spriteMask;

    private int healthMultiplier;
    public float health;
    private float startHealth;

    private float damageDealt = 0;

    private void Start()
    {
        animator.enabled = false;
        spritesBeforeBreak.Reverse();
        healthMultiplier = spritesBeforeBreak.Count;
        startHealth = health;
        if (healthMultiplier != 0)
            health *= healthMultiplier + 1;
    }

    public void TakeDamage(float damage)
    {
        damageDealt += damage;

        health -= damage;
        if (health <= 0)
        {
            animator.enabled = true;
            animator.SetTrigger("Break");
            Invoke(nameof(DisableCollider), 0.001f);

            if (spriteMask != null)
                spriteMask.SetActive(true);
            return;
        }

        if (damageDealt >= startHealth)
        {
            healthMultiplier--;
            spriteRenderer.sprite = spritesBeforeBreak[healthMultiplier];

            damageDealt -= startHealth;
        }
    }

    //Added this because sometimes the collider disable before pencil stuck on wall script uses it
    private void DisableCollider()
    {
        if (gameObject.GetComponent<Rigidbody2D>() != null)
            Destroy(gameObject.GetComponent<Rigidbody2D>());
        var colliders = gameObject.GetComponents<Collider2D>();

        for (int i = 0; i < colliders.Length; i++)
        {
            colliders[i].enabled = false;
        }
    }
}
```
</details>
