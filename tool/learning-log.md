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
    * First, I had

<!--
* Links you used today (websites, videos, etc)
* Things you tried, progress you made, etc
* Challenges, a-ha moments, etc
* Questions you still have
* What you're going to try next
-->
