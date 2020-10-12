<template>
  <div class="game">
    <StartPopup 
      v-if="isStartPopup" 
      @speed-saveGame="handle"/>
    <FailPopup 
      v-if="isFailPopup"/>
    <VictoryPopup 
      v-if="isVictoryPopup"/>
    <h1 class="game__title">Simon The Game</h1>
    <p class="game__currentLevel">Round: {{ count }}</p>

    <div class="game__board">
      <div class="game__center-circle">
        <p class="center-circle__name">Simon</p>
        <button 
          class="center-circle__btn" 
          @click="gameLevel">
          Start
        </button>
      </div>
      <div 
        id="red" 
        class="game-btn game-btn__red"  
        :class="{ 'red': red}" 
        @click="handleColorButton"></div>
      <div 
        id="blue" 
        class="game-btn game-btn__blue" 
        :class="{ 'blue': blue }" 
        @click="handleColorButton"></div>
      <div 
        id="green" 
        class="game-btn game-btn__green" 
        :class="{ 'green': green }" 
        @click="handleColorButton"></div>
      <div 
        id='yellow' 
        class="game-btn game-btn__yellow" 
        :class="{ 'yellow': yellow }" 
        @click="handleColorButton"></div>
    </div>
  </div>
</template>

<script>
import StartPopup from './StartPopup.vue';
import FailPopup from './FailPopup.vue';
import VictoryPopup from './VictoryPopup.vue';

export default {
  name: 'Game',
  components: {
    StartPopup,
    FailPopup,
    VictoryPopup,
  },
  data: () => ({
    green: false,
    red: false,
    yellow: false,
    blue: false,
    count: 0,
    step: 0,
    stepArrGame: [],
    stepArrPerson: [],
    isStartPopup: false,
    levelSpeed: "1500",
    colorBtn: ['red', 'green', 'blue', 'yellow'],
    maxLevel: 10,
    sounds: [
      new Audio(require('@/assets/audio/1.mp3')),
      new Audio(require('@/assets/audio/2.mp3')),
      new Audio(require('@/assets/audio/3.mp3')),
      new Audio(require('@/assets/audio/4.mp3')),
    ],
    isPlay: false,
    isFailPopup: false,
    isVictoryPopup: false,
  }),
  methods: {
    gameLevel() {
      this.isStartPopup = true;
    },
    handle(item) {
      this.levelSpeed = item;
      this.isStartPopup = false;
      this.isPlay = true;
      this.count = 0;
      this.step = 0;
      this.stepArrGame = [];
      this.stepArrPerson = [];
      this.addStep();
      setTimeout(() => this.playSequence(this.stepArrGame, this.levelSpeed), 500);
    },

    handleColorButton(e) {
      if (this.isPlay) {
        this.audioSingnal(e.target.id);
        this.lightColorButton(e.target.id);
        this.stepArrPerson.push(e.target.id);
        if (this.stepArrGame.slice()[this.step] === this.stepArrPerson.slice()[this.step]) {
          this.step++;
          if (this.step >= this.stepArrGame.length && this.stepArrGame.length < this.maxLevel) {
            setTimeout(() => {
              this.addStep();
              this.playSequence(this.stepArrGame, this.levelSpeed);
              this.stepArrPerson = [];
              this.step = 0;
            }, 1250);
          }
        } else {
          this.count = 0;
          this.isFailPopup = true;
          setTimeout(() => {
            this.isFailPopup = false;
          }, 2000);
          return;
        } 
      }
    },

    addStep() {
      const color = Math.floor(Math.random() * this.colorBtn.length);
      this.stepArrGame.push(this.colorBtn[color]);
      this.count++;
    },

    playSequence(arrStep, speed) {
      if (this.stepArrGame.length === this.maxLevel) {
        this.isVictoryPopup = true;
        setTimeout(() => {
          this.isVictoryPopup = false;
        }, 2500);
        return;
      } else {
        for (let i = 0; i < arrStep.length; i++) {
          setTimeout(() => {
            this.audioSingnal(arrStep[i]); 
            this.lightColorButton(arrStep[i]);
          }, i * speed);
        }
      }
    },

    audioSingnal(item) {
      this.sounds[this.colorBtn.indexOf(item)].play();
    },

    lightColorButton(item) {
      this[item] = true;
      setTimeout(() => {
        this[item] = false;
      }, 400);
    },

  },
};
</script>

<style scoped lang="scss">
  @import '../assets/style/Game.sass';
</style>
