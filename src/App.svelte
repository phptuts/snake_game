<script>
  import Snake from "./Snake.svelte";
  import Food from "./Food.svelte";
  let direction = "right";
  const height = 50;
  const width = 50;

  let foodLeft = 500;
  let foodTop = 300;

  let snakePositions = [];
  reset();

  $: score = snakePositions.length - 3;

  setInterval(() => {
    snakePositions.pop();
    let { left, top } = snakePositions[0];

    if (direction === "right") {
      left += 50;
    }
    if (direction === "left") {
      left -= 50;
    }

    if (direction === "up") {
      top -= 50;
    }

    if (direction === "down") {
      top += 50;
    }

    if (isCollide({ left: foodLeft, top: foodTop }, snakePositions[0])) {
      snakePositions.push(snakePositions[snakePositions.length - 1]);
      foodLeft = Math.ceil(Math.random() * 19) * 50;
      foodTop = Math.ceil(Math.random() * 13) * 50;
    }

    snakePositions = [{ top, left }, ...snakePositions];

    if (isGameOver()) {
      //alert("Game over");
      reset();
    }
  }, 200);

  function isCollide(a, b) {
    return !(
      a.top + 0 < b.top ||
      a.top > b.top + 0 ||
      a.left + 0 < b.left ||
      a.left > b.left + 0
    );
  }

  function isGameOver() {
    const head = snakePositions[0];
    const isSnakeTouchingItSelf = snakePositions
      .slice(1)
      .reduce((prev, next) => {
        return prev || isCollide(next, head);
      }, false);

    return (
      head.left < 0 ||
      head.top < 0 ||
      head.left > 950 ||
      head.top > 650 ||
      isSnakeTouchingItSelf
    );
  }

  function reset() {
    direction = "right";
    foodLeft = Math.ceil(Math.random() * 19) * 50;
    foodTop = Math.ceil(Math.random() * 13) * 50;
    snakePositions = [
      {
        left: 100,
        top: 0
      },
      {
        left: 50,
        top: 0
      },
      {
        left: 0,
        top: 0
      }
    ];
  }

  function onKeyboardEvent(e) {
    const { keyCode } = e;
    if (keyCode === 38) {
      direction = "up";
    } else if (keyCode === 39) {
      direction = "right";
    } else if (keyCode === 37) {
      direction = "left";
    } else if (keyCode === 40) {
      direction = "down";
    }
  }
</script>

<style>
  main {
    width: 1000px;
    height: 700px;
    border: solid black 1px;
    position: relative;
    margin: 20px auto;
    background-image: url("../background.jpg");
    background-size: cover;
  }
  h2,
  h1 {
    text-align: center;
  }
</style>

<h1>Snake Game</h1>
<main>
  <Snake {direction} {width} {height} bind:snakePositions />
  <Food top={foodTop} left={foodLeft} />
</main>
<h2>Score {score}</h2>
<svelte:window on:keydown={onKeyboardEvent} />
