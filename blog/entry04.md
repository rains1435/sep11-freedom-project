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


[Previous](entry03.md) | [Next](entry05.md)

[Home](../README.md)
