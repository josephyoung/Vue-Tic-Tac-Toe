<template functional>
  <button
    class="square"
    @click="props.handleClick"
    :style="props.squareStyle"
  >
    {{ props.value }}
  </button>
</template>

<style>
  .square {
    background: #fff;
    border: 1px solid #999;
    float: left;
    font-size: 2rem;
    font-weight: bold;
    line-height: 1rem;
    height: 3rem;
    margin-right: -1px;
    padding: 0;
    text-align: center;
    width: 3rem;
  }

  .square:focus {
      outline: none;
  }
</style>
