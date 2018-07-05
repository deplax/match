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
            <div class="md-layout-item md-size-50">
              <md-content class="md-elevation-1">
                <span class="timer center">00:00</span>
              </md-content>
              <md-field>
                <label>Number</label>
                <md-input type="number"></md-input>
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
                <md-button class="md-raised md-primary center start">start</md-button>
              </div>
            </div>
          </div>
        </div>

      </md-card-content>
    </md-card>
  </div>
</template>

<script>
  export default {}
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
