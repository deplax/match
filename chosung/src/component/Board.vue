<template>
  <div class="board_area">
    <md-card>
      <md-card-header>
        <div class="md-title">
          <md-icon>spellcheck</md-icon>
          <span>Board</span>
        </div>
      </md-card-header>

      <md-card-content>
        <div class="md-layout md-gutter">
          <div class="md-layout-item md-layout md-gutter md-alignment-center">
            <div class="md-layout-item md-size-20">
              <md-content class="md-elevation-1">
                <span class="text center">ㄱ</span>
              </md-content>
            </div>
            <div class="md-layout-item md-size-20">
              <md-content class="md-elevation-1">
                <span class="text center">ㄴ</span>
              </md-content>
            </div>
            <div class="md-layout-item md-size-20">
              <md-content class="md-elevation-1">
                <span class="text center">ㄷ</span>
              </md-content>
            </div>
          </div>
        </div>

        <div class="md-layout md-gutter">
          <div class="md-layout-item md-layout md-gutter md-alignment-center">
            <div class="md-layout-item md-size-40">
              <md-field>
                <label for="age">count</label>
                <md-input type="number" id="age" name="age" autocomplete="age"/>
                <span class="md-error">The age is required</span>
                <span class="md-error">Invalid age</span>
              </md-field>
            </div>
            <div class="md-layout-item md-size-30">
              <md-card-actions>
                <md-button>Create</md-button>
              </md-card-actions>
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
  .board_area {
    padding: 15px 15px 15px 15px;
  }

  .center {
    display: table;
    margin-left: auto;
    margin-right: auto;
  }

  .text {
    line-height: 60px;
    font-size: 50px;
  }

</style>
