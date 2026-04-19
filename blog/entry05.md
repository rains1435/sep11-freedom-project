# Entry 5: CREATION OF MVP
##### 4/18/26

## What more more MORE have I learned?

### Key System
My game had no objective other than jumping around on obstacles and collecting coins that do nothing. So I decided to add keys and keys are fun to play with because now I can make obstacles that players have to beat in order to reach the key which is used to unlock a door!
``` js
// key
key = this.physics.add.staticImage(410, 370, 'key');
key.setSize(16, 36);
key.setScale(0.15);

// door
door = this.physics.add.staticImage(900, 274, 'doorClosed');
door.setSize(45, 54);
door.setScale(0.6);
barrier = this.physics.add.collider(player1, door);

// pick up key
this.physics.add.overlap(player1, key, function() {
    key.destroy();
    keyOn = true;
    this.physics.world.removeCollider(barrier);
}, null, this);

// unlock door
this.physics.add.overlap(player1, door, function() {
    if (keyOn == true) {
        door.setTexture('doorOpen');
        keyOn = false;
    }
}, null, this);
```
* **Step one:** create a key and don't make it gigantic (also setSize works with the hitboxes, scale doesn't)
* **Step two:** Make a collidable door with `.collider()`; relationship set between door and the player (why? Collidable because without it, user can just walk through the door without the key)
* **Step three:** USE THE LOVELY `.overlap` physics on the key and player so when both overlaps, the key literally disappears (`.destroy`) and you have picked up the key. Also why do I remove the collider for the door after the key is collected? To be honest, it won't work otherwise. I originally tried removing the barrier inside the "unlock door" `overlap` but it didn't work out since after collecting the keys and trying to unlock the door, the barrier was still there. So I decided to put the `this.physics.world.removeCollider(barrier);` inside "pick up key" overlap. I mean the barrier doesn't really matter anymore after you have the keys so why not remove it... it's not like there's a second player.
* **Step four:** AGAIN... USE THE LOVELY `.overlap` physics but now for unlocking the door. If the player has picked up the key (has the key on them), then when player overlaps with the door, the door opens (literally because the images changes from `doorClosed` to `doorOpen`) and the key the player held onto kind of disappears (key used once = no more!). Also note that the key wasn't used to open the door because for Step three, the door opened once the player picks up the key (visually appealing for the door to open).

### Portal System

If you didn't know, I've added levels ([CLICK ME TO CHECK OUT HOW I MADE LEVELS](../tool/learning-log.md) -> **3/29/26**)

I made levels! But levels are useless if the player cannot access it... Wait what if I made a teleportation portal inspired from the Minecraft Nether Portal?!

``` js
// levels

// player is in here!
class Level1 extends Phaser.Scene {
    constructor() {
        super('Level1');
    }

    preload() {
        // some textures #1
    }

    create() {
        // very cool map #1
    }

    update() {
        // wasd keys movement
    }
}

// player walks and touches the portal and now their in level 2!
class Level2 extends Phaser.Scene {
    constructor() {
        super('Level2');
    }

    preload() {
        // some textures #2
    }

    create() {
        // very cool map #1
    }

    update() {
        // wasd keys movement
    }
}
```

Let's say I have two VERY beautiful and DEFINITELY not empty levels (each with its own map). After the player unlocks the door with the key they have, they walk towards the portal to enter level 2...

``` js
// portal
teleport = this.physics.add.staticGroup();
portal = teleport.create(975, 113, 'portal');
portal.setSize(50, 80);
portal.setScale(0.15);
portal.refreshBody();

this.physics.add.overlap(player1, portal, function() {
    if (score >= coinValue * 10) {
        alert("YOU BEAT THE FINAL LEVEL!!!");
        userAnswered = false;
        keyOn = false;
        score = 0;
        this.scene.start('Ending');
    }
}, null, this);
```

* At the instant the player touches the portal, they teleport to level 2! *"But Rain, what actually happens???"*
* `.overlap` physics comes in as the main character for doing figuring out these player to object interactions (clap it up for them!). The system reads that the player has overlapped with the portal, vice versa and what it does is it runs a special function. That special function is that if the player HAS COLLECTED all the coins and their scores match that value after all coins collected, it will RESET EVERYTHING YOU HAVE ON YOU and alerts you with a message that you're moving onto the next level (and you teleport because of `this.scene.start('Ending');` -> stops the current scene to teleport you to the target scene -> [Learn More](https://docs.phaser.io/phaser/concepts/scenes#start)).

## COMPLETED MVP VERSION OF OUR GAME

### What did we do?

LINK TO THE PREVIEW -> [**GAME**](https://rains1435.github.io/our-first-game/)

Previously in [Blog 4](entry04.md), I said that we will learn everything first before applying in our game. So me and my partner Xin Yu stuck to that plan and we started making the game over the spring break.

Issue was that I was busy during spring break and so although Xin Yu and me were able to set up the Death System, Textures, and Basic Mechanics of the game, it was due to my absence during most of the spring break that we had to do it the day before. So the day before the due date (4/12/26), we called and decided to finish the majority of the game in 7 hours I believe. I thought we weren't going to finish but you know what the surprise was? WE FINISHED IT JUST IN TIME!!! You may ask us how? It's because the plan we stuck with worked out. We knew all the code necessary for the game and THANKFULLY, we have a MVP plan so we weren't stuck.

### What external tools did we use?

I'll be 100% transparent here because a guy always have ways of doing things. I googled a lot on how to make key systems and things of that sort. I found some great documentations (Some of the linked words link to documentations I found on google!).  However, it would've been impossible with the use of AI. Remember how the due date was literally "tommorow"? Yeah WE HAD THE KNOWLEDGE but WE AREN'T PERFECT ALRIGHT? We had errors along the way so we needed AI to debug them for us (**WE USED GOOGLE OVERVIEW AI WHICH WAS A BAD OPTION BUT THAT'S ALL WE HAD**). Sometimes the error would so tiny that it would take us 10 minutes if we actually went to look for it. GOOGLE AI OVERVIEW wasn't the best because it kept giving us wrong recommendations and there's a text limit apparently so we had to copy and paste chunk by chunk.

**For example:**

``` js
this.physics.add.overlap(player1, spikes, function() {
    if (dying === false) {
        dying = true;
        player1.disableBody(true, false);
        lives--;
        livesText.setText('Lives: ' + lives);
        score = 0;
        scoreText.setText('Score: 0');
        if (lives <= 0) {
            lives = 3;
            dying = false;
            userAnswered = false;
            keyOn = false;
            this.scene.start('Level1');
        } else {
            this.time.addEvent({
                delay: 500,
                callback: function() {
                    dying = false;
                    userAnswered = false;
                    keyOn = false;
                    this.scene.restart();
                },
                callbackScope: this
            });
        }
    }
}, null, this);
```

There was an issue with the death system. Whenever the player touched the spikes, they would sometimes lose 2 lives. I figured out that it was the invisible hitboxes I made for it (3 mini hitboxes, each one on one of the three vertices). Sometimes the player would touch 2 hitboxes which equals two lives lost. I was lost and being completely honest, this was the only time where I had AI help me "write a code" (I was guided through it; not given the answer). I asked Google along with my code and that I had that weird hitbox issue: "Without telling me the answer, what can I start to do?" It told me to try to write a code where there was a pause when the player FIRST touches a hitbox (not 2). I didn't know how to do the delay part so I asked for it to give me some starter code but instead it straight up gave me the answer to the code (accidentally). You know me, I took what it gave me and asked it "what does this code do? I want to learn?"

**Code I am talking about:**
``` js
this.time.addEvent({
    delay: 500,
    callback: function() {
        dying = false;
        userAnswered = false;
        keyOn = false;
        this.scene.restart();
    },
    callbackScope: this
});
```

It basically told me that whenever your player "dies", it will run some event where the whole scene pauses for a 500ms (you get to see the death frame), then the system reads what's inside the `callback: function(){}` (`callbackScope: this` is necessary because it tells `this.scene.restart();` what scene to restart). Scene restarts after the 500ms is over. An analogy that I got from it was imagine the `delay` as the calming of a storm (pauses the scene to prevent double trigger of death hitbox), the `callback` being a note with a little label (`callbackScope: this`) on what world (scene) to restart specifically.


---

## Engineering Design Process


[Previous](entry04.md) | [Next](entry06.md)

[Home](../README.md)
