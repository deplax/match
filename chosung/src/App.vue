<template>
  <div id="app">
    <Header></Header>
    <Board></Board>
    <Timer v-on:updateStatus="updateStatus"></Timer>
  </div>
</template>

<script>
  import Header from './component/Header'
  import Board from './component/Board'
  import Timer from './component/Timer'

  export default {
    data() {
      return {
        gameStatus: "READY"
//        READY, PLAY, END
      }
    },
    methods: {
      updateStatus(status) {
        this.gameStatus = status;
      },
    },
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
