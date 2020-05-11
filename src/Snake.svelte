<script>
  import SnakeBody from "./SnakeBody.svelte";
  export let snakePositions = [];
  export let height;
  export let width;
  export let direction = "right";
</script>

{#each snakePositions as position, i}
  <SnakeBody
    isHead={i === 0}
    {width}
    {height}
    {direction}
    left={position.left}
    top={position.top} />
{/each}
