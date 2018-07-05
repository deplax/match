<template>
  <div id="app">
    <Header></Header>
    <Board></Board>
    <Timer></Timer>
  </div>
</template>

<script>
  import Header from './component/Header'
  import Board from './component/Board'
  import Timer from './component/Timer'

  export default {
    components: {
      "Header": Header,
      "Board": Board,
      "Timer": Timer,
    }
  }
</script>

<style>
  .md-primary {
    background-color: #000;
  }
</style>
