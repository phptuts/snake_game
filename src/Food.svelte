<script>
  export let left = 100;
  export let top = 200;
</script>

<style>
  .food {
    width: 50px;
    height: 50px;
    position: absolute;
    border: solid black 1px;
    background-color: red;
    border-radius: 50%;
    z-index: 0;
  }
</style>

<div style="left: {left}px; top: {top}px;" class="food" />
