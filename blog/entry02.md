# Entry 2: LEARNING PHASE
##### 12/20/25

## What have I learned from practicing with Phaser?
I have learned A LOT about how phaser works and what to do in a situation where I have to build a minigame. The knowledge isn't 100% yet but I do know how to do more than creating a canvas with a background. So let's get started...

-> **[FOLLOW ALONG](../tool/learning-log.md)** <-

*Note: I will show SOME parts that I think are important in this blog, not everything*

### Platforms
After learning how to add a background of a beautiful sky in my canvas, I would create actual platforms (**like the ones you'll see in some arcade game in the early 2000s**). It was actually very easy to create it since all I had to do was, like the background, save an image of a platform on google and put it in my `assets` folder to which I can preload it for use. Below is a full breakdown of the next steps:

``` js
function create ()
{
    let platforms = this.physics.add.staticGroup(); // platform is immovable/static and collidable

    platforms.create(400, 568, 'ground').refreshBody(); // The ground with x and y coordinates; separate entity from the platforms code below it

    // Since I want 3 platforms with same size, I created a function to refactor.
    function ground (x,y) {
    return platforms.create(x, y, 'ground') // so each platform can have their own position
        .setDisplaySize(300, 250) // hard-coded size = same size
        .refreshBody();
    }

    // Calls ground function = same size but argument are different for position x,y
    ground(650, 400);
    ground(150, 250);
    ground(700, 170);
}
```

**RESULT:**

![ll3](../tool/ss/ll3.jpg)

### Sprite and Physics/Collision
The world of platforms looks boring so I added a frog sprite that can collide with platforms and fall like there's gravity. As so, save image, put into `assets`, preload for use. Now look below:

``` js
//in the create function
let player = this.physics.add.sprite(350, 100, 'frog'); // frog sprite is collidable and is a sprite entity
player.setScale(0.07).setBounce(0.2).setCollideWorldBounds(true); // frog is scaled smaller for fit, there's bounce when hit the floor, and can collide
this.physics.add.collider(player, platforms); // collision between the frog and platforms now works
```

Struggle: there was an issue with the way the platform image was originally and that was it had extra space around it. This made collision a little weird because the frog would be a few feet up from the actual platform. Simply, I cropped the platform image. Also the ground platform (separate) needed to be its own variable or else mix up can happen between ACTUAL platforms and the ground platform: `let floor = platforms.create(400, 568, 'ground').refreshBody(); floor.setDisplaySize(800, 100);`

### Sprite Movement
A world without movement would be lifeless so I gave the frog the ability to move around but with a twist... it is controlled by the user via the arrow keys.
```js
function update () {
    cursors = this.input.keyboard.createCursorKeys(); // lets phaser be aware to detect arrow keys
    if (cursors.left.isDown) // left arrow
    {
        player.setVelocityX(-160); // speed when moving left

        player.anims.play('left', true); // left moving animation
    }
    else if (cursors.right.isDown) // right arrow
    {
        player.setVelocityX(160); // speed when moving right

        player.anims.play('right', true); // right moving animation
    }
    else
    {
        player.setVelocityX(0); // not moving; rest

        player.anims.play('turn'); // rest animation
    }

    if (cursors.up.isDown && player.body.touching.down) // up arrow
    {
        player.setVelocityY(-330); // jumping
    }
}
```

This wouldn't work and here's why
* I only have one frame of the frog so animations would be unnecessary and cause an error shown in the console as "missing animation"
* Since the `player` variable is specifically nested inside the `create` function, I couldn't really use it in the `update` function. So I had to make the `player` variable global, thus outside the `create` function. The same applies for the `cursor` variable which isn't seen in the code above.

``` js
    // global variables so it's accessible/ can be used by functions
    var cursors;
    var player;
    ...
    // in function update, no more animations -> player.anims.play()
    function update ()
    {
        cursors = this.input.keyboard.createCursorKeys();
        if (cursors.left.isDown) // left arrow
        {
            player.setVelocityX(-160); // speed when moving left
        }
        else if (cursors.right.isDown) // right arrow
        {
            player.setVelocityX(160); // speed when moving right
        }
        else
        {
            player.setVelocityX(0); // rest
        }

        if (cursors.up.isDown && player.body.touching.down) // up arrow
        {
            player.setVelocityY(-330); // jumping
        }
    }
```

## Winter Goals

Christmas is just around the corner and I am so so excited to finally take a break from school. However, I will be setting some goals for the freedom project over this winter break.

**Over this winter break, I will...**
* Try to learn more phaser material such as learning how to add a point system via collecting something
* Practice with phaser; maybe create a mini project? Maybe a points-based game with obstacle course?
* Brainstorm ways to create my final freedom project game; think of how to make the game fun and logic-based
* Try to communicate with my partner Xin Yu to maybe help him catch up since he was out for a few weeks
* Conduct a survey to gather some opinions on boredom and logical/puzzle games via google forms

---

## Engineering Design Process (EDP)

I am on the second step, **Research the problem**, of the EDP. The problems are boredom and the lack of logical games viewed as hardwork rather than fun. To see some proof of this, I will conduct a survey over the winter break on these problems. The purpose is to collect data on the frequency of boredom and opinions on logical games to determine whether boredom and negative outlooks of logical games are common problems. Of course, similar to last year, I will be walking around my neighborhood but instead of asking, I will interest them in taking a google form survey.

## Skills

### Consideration
This is an important skill to address and it's because I was thinking about doing the "Research the problem" part via my own personal experience which isn't enough of an evidence to determine that my problem is actually an problem. Thus I had to take other people's viewpoints on boredom and logical games to somewhat confirm that the problem is or isn't a problem. The purpose of a survey is that the problem a personal issue with yourself but an issue that impacts more than one person. If I had done personal experience (1 opinion), that would either COMPLETELY make it a problem or not a problem which is a very delusional outlook. Imagine saying that everyone hates dogs because I hate dogs... That would be absolutely ridiculous. Overall, I had to consider for this part of the EDP.

### How to Google
For many of the learning logs I've done to learn phaser, I've used google and sometimes CHATGPT to figure out certain issues. Now before calling me a cheater and a lazy bum, I am simply trying to save time because I have other priorities in life and I am not using it to give me answers as giving me answers would do nothing in my learning process; will worsen my cognitive functions. Just wanted to say that if anyone thought I'd cheat. For instance, I would use Google to find if there are documentations of how to implement WASD keys into sprite movement for phaser and I found a [website](https://phaser.discourse.group/t/wasd-keyboard-movement-phaser-3/8297/2#:~:text=Key%2C%20D%3A%20Key%20%7D-,var,-keys%20%3D%20this.input) that showed me. Now if google can't solve an issue, I would then move onto ChatGPT for **ASSISTANCE**. Once my console was mass printing error message: "missing animation" and I didn't know what that meant so I asked ChatGPT "Why is there missing animation error code Phaser" and it told me that I probably don't have animation preloads for those animation frames. I double checked the code and found out I used: `player.anims.play()` even though I had no preloads for it. I removed them and problem fixed. See how no copy and pasting of my FULL CODE was done? Yeah that's part of the learning process; you ask AI a RELATED question that doesn't reveal the answer. Thank me later.

## Next Step
After collecting data from my survey over the winter break, I'll probably on the 3rd Step: **Brainstorm possible solutions** of the EDP. For that step, I am still in the unknown for it because I don't have data collected to make a valid conclusion. Stay tuned for results!

**I'LL SEE YOU NEXT YEAR!!**

[Previous](entry01.md) | [Next](entry03.md)

[Home](../README.md)
