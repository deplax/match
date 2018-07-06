<template>
  <div class="timer_area">
    <md-card>

      <md-card-header>
        <div class="md-title">
          <md-icon>timer</md-icon>
          <span>Timer</span>
        </div>
      </md-card-header>

      <md-card-content>
        <div class="md-layout md-gutter">
          <div class="md-layout-item md-layout md-gutter md-alignment-center">
            <div class="md-layout-item md-size-60">
              <md-content class="md-elevation-1">
                <span class="timer center">00.000</span>
              </md-content>
              <md-field>
                <label>Number</label>
                <md-input type="number" v-model.number="count"></md-input>
              </md-field>
            </div>
          </div>
        </div>

        <div class="md-layout md-gutter">
          <div class="md-layout-item md-layout md-gutter md-alignment-center">
            <div class="md-layout-item">
              <md-card-actions class="center">
                <md-button>pause</md-button>
                <md-button>stop</md-button>
              </md-card-actions>
            </div>
          </div>
        </div>

        <div class="md-layout md-gutter">
          <div class="md-layout-item md-layout md-gutter md-alignment-center">
            <div class="md-layout-item md-size-95">
              <div>
                <md-button class="md-raised md-primary center start" v-on:click="start">start</md-button>
              </div>
            </div>
          </div>
        </div>

      </md-card-content>
    </md-card>
  </div>
</template>

<script>
  let timerMillisecond = 1000 * 10;
  let timerTime = Date.now() + timerMillisecond;
  let diff = timerTime - Date.now();
  let displaySecond = (diff % (1000 * 60)) / 1000;
  let displayMilisecond = diff % 1000;

  export default {
    data() {
      return {
        count: 10,
        currentTime: 0,
        timerStatus: "STOP"
      }
    },
    methods: {
      start() {
        let timerMillisecond = 1000 * this.count;
        let timerTime = Date.now() + timerMillisecond;

        const timer = setInterval(function(){
          let diff = timerTime - Date.now();
          let displaySecond = (diff % (1000 * 60)) / 1000;
          let displayMillisecond = diff % 1000;
          console.log(displaySecond + ":" + displayMillisecond / 100)
        }, 10);
      },
      stop() {

      },
      pause() {

      }
    }
  }
</script>

<style scoped>
  .start {
    height: 100px;
    width: 100%;
  }

  .center {
    display: table;
    margin-left: auto;
    margin-right: auto;
  }

  .timer_area {
    padding: 15px 15px 15px 15px;
  }

  .timer {
    line-height: 60px;
    font-size: 50px;
  }
</style>
