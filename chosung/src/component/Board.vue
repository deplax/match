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
            <div v-for="chosungCard in chosungCardList" class="md-layout-item md-size-20">
              <md-content class="md-elevation-1">
                <span class="text center">{{chosungCard}}</span>
              </md-content>
            </div>
          </div>
        </div>

        <div class="md-layout md-gutter">
          <div class="md-layout-item md-layout md-gutter md-alignment-center">
            <div class="md-layout-item md-size-40">
              <md-field>
                <label>count</label>
                <md-input type="number" v-model.number="count"/>
                <span class="md-error">The age is required</span>
                <span class="md-error">Invalid age</span>
              </md-field>
            </div>
            <div class="md-layout-item md-size-30">
              <md-card-actions>
                <md-button v-on:click="create">Create</md-button>
              </md-card-actions>
            </div>
          </div>
        </div>
      </md-card-content>

    </md-card>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        count: 2,
        chosungCardList: ["?", "?"]
      }
    },
    methods: {
      create() {
        const DEFAULT_COUNT = 2;
        const MIN_COUNT = 1;
        const MAX_COUNT = 5;
        const CHOSUNG_LIST = "ㄱㄴㄷㄹㅁㅂㅅㅇㅈㅊㅋㅌㅍㅎ".split("");

        let count = this.getValue(this.count, MIN_COUNT, MAX_COUNT, DEFAULT_COUNT);

        this.chosungCardList = [];
        for(let i = 0; i < count; i++){
          let index =  this.randomInt(0, CHOSUNG_LIST.length - 1);
          this.chosungCardList.push(CHOSUNG_LIST[index])
        }
      },
      randomInt(from, to) {
        return Math.floor((Math.random()*(to - from + 1)) + from);
      },
      getValue(value, min, max, defaultValue){
        if (!Number.isInteger(value)){
          return defaultValue;
        }
        if (value < min) {
          return min
        }
        if (value > max) {
          return max
        }
        return value
      }
    }
  }
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
