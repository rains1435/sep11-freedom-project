# Entry 4: PLANNING PHASE
##### 3/13/26

## What more MORE have I learned about Phaser?

### [Score System](https://phaser.io/tutorials/making-your-first-phaser-3-game/part9)
Yes yes YES it's finally here... a score system that is connected to the very shiny coins I've added to the game. Originally, I thought it would be a difficult process to make a score system but one place I forgot to double check was the Phaser page because I found out they literally teach you how to make a score system (click the header for the link). **BELOW IS EXAMPLE:**

``` js
var score = 0;
var scoreText;

function create ()
{
    // a score visual that pops up in the corner of your canvas
    scoreText = this.add.text(16, 16, 'score: 0', { fontSize: '32px', fill: '#000' });
    // you're adding onto an already existing function that I previously made (the log above this one)
    function collectCoin (player1, coins)
    {
        coins.disableBody(true, true);

        score += 10;
        scoreText.setText('Score: ' + score);
    }
}
```

The score system is like an add-on to the code that collects coins. So the function `collectCoin` runs as so: When player collides with a coin, the coin's body is disabled/disappears and it add +10 to the score board displayed via `.setText('Score: ' + score)`.

### Death System
Well this one was much more difficult to make. Originally, I visited the Phaser site to search for it. In the "Making your first Phaser 3 game", there was the "[Bouncing Bombs](https://phaser.io/tutorials/making-your-first-phaser-3-game/part10)" part and although it had a death system, it was not what I was looking for because their "death" subject was a bomb that MOVED (I wanted a static spike) and the "game over" death (I wanted a respawn death). So after spending 30 minutes of my life of trying to figure out a way to make a death system that respawns via collision with spikes, **here's what I made:**

``` js
var spikes;
var spikeCreate;
function create()
{
    spikes = this.physics.add.staticGroup();
    spikeCreate = spikes.create(200, 210, 'spikes');
    spikeCreate.setScale(0.4).refreshBody();
    this.physics.add.overlap(player1, spikes, function() {
        player1.setPosition(350, 400);
        score = 0;
        scoreText.setText('Score: 0');
    }, null, this);
}
```
**Breakdown:**
* Created 2 global variables (necessary)
* `spikes = this.physics.add.staticGroup();` makes it an immovable; not affected by gravity
* `spikeCreate = spikes.create(200, 210, 'spikes');` creates a spike at a position
* `this.physics.add.overlap(player1, spikes, function() { player1.setPosition(350, 400); score = 0; scoreText.setText('Score: 0'); }, null, this);` similar to the coins overlapping, it looks for when `player1` comes into contact with `spikes` vice versa. When it does happen, it runs a function to which `player1` respawns at original spawn position of `(350, 400)`, resetting user's score to 0. `null` and `this` are necessary to include; no explanation because I don't know much about it.

That's all the major things I've learned using Phaser! Thanks! now let's move on...

## MVP Progress

The score and death system are progress of MVP. Why? Just look at my long plan... Well I am not going to copy and paste it here so just click on this link -> [HERE](../../our-first-game/plan.md)

I made one change to the plan and that is I am removing the dates of which we have to do each part of the MVP. Reason is that I AM VERY BUSY WITH SCHOOL. Setting these deadlines is putting more pressure on me and I don't want to stress about it constantly. New plan is that me and my partner Xin Yu will learn everything we need for the MVP based on the plan on our own time but NO PROCRASINATING. It seems like this plan is working better because I've already learned how to make a score and death system which meets 2 of our major game MVP parts.

## Engineering Design Process




[Previous](entry03.md) | [Next](entry05.md)

[Home](../README.md)
