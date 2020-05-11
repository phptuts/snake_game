<script>
  export let top;
  export let left;
  export let width;
  export let height;
  export let isHead = false;
  export let direction;
</script>

<style>
  .snake-body {
    background-color: green;
    border: black 1px solid;
    position: absolute;
    z-index: 3;
  }
  .eyes {
    position: absolute;
    background-color: orange;
    border-radius: 50%;
    width: 20px;
    height: 20px;
  }
  #leftEye {
    left: 10px;
    top: 2px;
  }
  #rightEye {
    left: 10px;
    bottom: 2px;
  }
  .snake-body.right {
    transform: rotate(0deg);
  }
  .snake-body.left {
    transform: rotate(180deg);
  }
  .snake-body.up {
    transform: rotate(90deg);
  }
  .snake-body.down {
    transform: rotate(90deg);
  }
</style>

<div
  style="left: {left}px; top: {top}px; width: {width}px; height: {height}px;"
  class="snake-body {direction}">
  {#if isHead}
    <div id="leftEye" class="eyes" />
    <div id="rightEye" class="eyes" />
  {/if}
</div>
