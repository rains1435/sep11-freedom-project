# Tool Learning Log

## Tool: **Phaser**

## Project: **Game**

---

### 10/3/25:
* I learned how to create a game canvas
  * First I'll need the "**starting"** code from [**Phaser**](https://phaser.io/tutorials/making-your-first-phaser-3-game/part1#:~:text=var%20config%20%3D%20%7B%0A%20%20%20%20type%3A%20Phaser.AUTO%2C%0A%20%20%20%20width%3A%20800%2C%0A%20%20%20%20height%3A%20600%2C%0A%20%20%20%20scene%3A%20%7B%0A%20%20%20%20%20%20%20%20preload%3A%20preload%2C%0A%20%20%20%20%20%20%20%20create%3A%20create%2C%0A%20%20%20%20%20%20%20%20update%3A%20update%0A%20%20%20%20%7D%0A%7D%3B%0A%0Avar%20game%20%3D%20new%20Phaser.Game(config)%3B)
  ``` js
    var config = {
        type: Phaser.AUTO,
        width: 800,
        height: 600,
        scene: {
            preload: preload,
            create: create,
            update: update
        }
    };

    var game = new Phaser.Game(config);
  ```
  * `type: Phaser.AUTO` is the game canvas or the screen where the user will see all the content. Adding `width: 800` and `height: 600` will size the game canvas
  * However, I want my game canvas to be in the center of the page so it requires some css and Phaser code:
  ``` html
    <style>
        /* CSS */
        html, body {
            margin: 0;
            padding: 0;
            width: 100%;
            height: 100%;
            display: flex;
            justify-content: center;
            align-items: center;
            background-color: green;
        }
        #game-container {
            width: 100%;
            height: 100%;
            display: flex;
            justify-content: center;
            align-items: center;
        }
    </style>
    <script>
        var config = {
            type: Phaser.AUTO,
            scale: {
                mode: Phaser.Scale.FIT,
                parent: 'game-container',
                width: 800,
                height: 600,
            },

            scene: {
                preload: preload,
                create: create,
                update: update
            }
        };

        var game = new Phaser.Game(config);
    </script>
  ```
**Result:**
![canvas](ss/ll1.jpg)


### 10/27/25:
* I learned how to add an background... but in my way!
  * Before I reveal my own method, I hit a obstacle and that was the assets for backgrounds wouldn't load
``` js
// these aren't the exact example, I just took parts of the phaser code to use as example.
function preload ()
{
    this.load.image('sky', 'assets/sky.png');
}

function create ()
{
    this.add.image(400, 300, 'sky');
}
```
* **The issue:** I don't have the phaser assets folder downloaded into my html page. This means I'll have to create my own folder.
* **The solution:** I created a directory/folder called `assets` in my `tool` parent directory. Then I downloaded a sky image online and put it into `assets`. Lastly...

**My "Method":**
``` js
function preload ()
{
    this.load.image('sky', 'assets/sky.jpg');
}

// 'sky' = the name of the image
// 'assets/sky.jpg' = access the assets folder then grabs the sky.jpg file

function create ()
{
    let sky = this.add.image(400, 300, 'sky');
    sky.setDisplaySize(800, 600);
}
// To summarize, the sky image is given a position of (400, 300) which is the center of the canvas. Then it is given the same size of the canvas so it is the background.
```

**Result:**
![background](ss/ll2.jpg)

### 11/15/25
* I found out how to add ACTUAL platforms to my canvas!
* Here's where I went to get the starter code: [The Platforms](https://phaser.io/tutorials/making-your-first-phaser-3-game/part4)
    * First I found an ground 2d image online, put it in my [assets](assets/ground.jpg) folder, and then preloaded it for future use
    * Then I pasted the starter codes into the create function
``` js
function create()
{
    platforms = this.physics.add.staticGroup();
    platforms.create(400, 568, 'ground').setScale(2).refreshBody();
    platforms.create(600, 400, 'ground');
    platforms.create(50, 250, 'ground');
    platforms.create(750, 220, 'ground');
}
```
* `platforms = this.physics.add.staticGroup` = gives "platform" or a group of "platforms" collision and is completely immovable by any other external factors.
* `.setScale(2)` = size scaling
* `.refreshBody()` = updates the "platforms" collision hitbox so it fits the new size/ position
* `platforms.create()` = create a "platform" and can give it (x, y) location + the preload name.
* I did some changes because the copied code didn't meet my expectations
    * Only scaled the size of first platform shown in this code while the rest are just default; they're really big on my screen and I wanted to resize it.
    * Plan: One big ground as the floor and 3 same sized platforms located differently
``` js
function create ()
{
    let platforms = this.physics.add.staticGroup(); // Changes to variable; can prevent errors and more

    platforms.create(400, 568, 'ground').refreshBody(); // The ground; separate entity from the platforms code below it

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

**Result:**
![background](ss/ll3.jpg)


<!--
* Links you used today (websites, videos, etc)
* Things you tried, progress you made, etc
* Challenges, a-ha moments, etc
* Questions you still have
* What you're going to try next
-->
