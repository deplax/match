<template>
  <div class="timer_area">
    <md-card>
      <md-progress-bar class="md-accent" md-mode="determinate" :md-value="percent"></md-progress-bar>

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
                <span class="timer center">{{displayTime}}</span>
              </md-content>
              <md-field>
                <label>Number</label>
                <md-input type="number" v-model.number="count" v-on:change="changeInput"></md-input>
              </md-field>
            </div>
          </div>
        </div>

        <div class="md-layout md-gutter">
          <div class="md-layout-item md-layout md-gutter md-alignment-center">
            <div class="md-layout-item">
              <md-card-actions class="center">
                <md-button v-on:click="pause">pause</md-button>
                <md-button v-on:click="stop">{{stopButtonText}}</md-button>
              </md-card-actions>
            </div>
          </div>
        </div>

        <div class="md-layout md-gutter">
          <div class="md-layout-item md-layout md-gutter md-alignment-center">
            <div class="md-layout-item md-size-95">
              <div>
                <md-button class="md-raised md-primary center start" v-on:click="start">{{startButtonText}}</md-button>
              </div>
            </div>
          </div>
        </div>

      </md-card-content>
    </md-card>
  </div>
</template>

<script>

  const DEFAULT_TIME = "00.000";
  const GameStatus = {
    READY: "READY",
    PLAY: "PLAY",
    END: "END"
  };

  const TimerStatus = {
    READY: "READY",
    RUN: "RUN",
    PAUSE: "PAUSE"
  };

  const StopButtonText = {
    STOP: "STOP",
    CLEAR: "CLEAR"
  };

  const StartButtonText = {
    START: "START",
    NEXT: "NEXT",
    END: "END"
  };

  let timer;

  export default {
    data() {
      return {
        percent: 0,
        count: 10,
        remainTime: 0,
        timerTime: 0,
        timerStatus: TimerStatus.READY,
        gameStatus: GameStatus.READY,
        displayTime: "",
        progress: "",
        stopButtonText: StopButtonText.STOP,
        startButtonText: StartButtonText.START
      }
    },
    methods: {
      start() {

        let self = this;

        if (self.timerStatus === TimerStatus.PAUSE) {
          self.timerTime = Date.now() + self.remainTime;
        } else {
          let timerMillisecond = 1000 * this.count;
          self.remainTime = timerMillisecond;
          self.timerTime = Date.now() + self.remainTime;
        }

        if ((self.timerStatus === TimerStatus.READY || self.timerStatus === TimerStatus.PAUSE)
          && (self.gameStatus === GameStatus.READY || self.gameStatus === GameStatus.PLAY)) {
          self.timerStatus = TimerStatus.RUN;
          self.gameStatus = GameStatus.PLAY;
          self.startButtonText = StartButtonText.NEXT;

          timer = setInterval(function () {
            let diff = self.timerTime - Date.now();
            self.remainTime = diff;
            let displaySecond = (diff % (1000 * 60)) / 1000;
            let displayMillisecond = diff % 1000;
            let displayText = Math.floor(displaySecond, 0).toString().padStart(2, "0") + "." + displayMillisecond.toString().padStart(3, "0");

            self.percent = self.getPercent(self.count * 1000, diff);

            if (diff <= 0) {
              self.timeUp();
            } else {
              self.displayTime = displayText;
            }
          }, 10);
        } else if (self.timerStatus === TimerStatus.RUN && self.gameStatus === GameStatus.PLAY) {
          let timerMillisecond = 1000 * this.count;
          self.timerTime = Date.now() + timerMillisecond;
        }
      },
      timeUp() {
        clearInterval(timer);
        this.timerStatus = TimerStatus.READY;
        this.gameStatus = GameStatus.END;
        this.stopButtonText = StopButtonText.CLEAR;
        this.startButtonText = StartButtonText.END;
        this.initDisplay();
      },
      stop() {
        clearInterval(timer);
        this.timerStatus = TimerStatus.READY;
        this.gameStatus = GameStatus.READY;
        this.stopButtonText = StopButtonText.STOP;
        this.startButtonText = StartButtonText.START;
        this.initDisplay();

      },
      pause() {
        if (this.timerStatus === TimerStatus.RUN) {
          this.timerStatus = TimerStatus.PAUSE;
          clearInterval(timer);
        } else if (this.timerStatus === TimerStatus.PAUSE) {
          this.start();
        }
        this.updateStatus("UPDATE");
      },
      updateStatus(status) {
        this.$emit("updateStatus", status);
      },
      initTimer: function () {
        this.initDisplay();
      },

      changeInput: function () {
        this.count = Math.round(this.count);
        this.count = Math.abs(this.count);

        if (this.count > 99) {
          this.count = 99;
        }
        this.initDisplay();
      },
      initDisplay: function () {
        this.displayTime = this.count.toString().padStart(2, "0") + ".000"
      },
      getPercent: function (settingTime, currentTime) {
        return 100 - currentTime / settingTime * 100
      },
    },
    mounted: function () {
      this.initTimer();
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
