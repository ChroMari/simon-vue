<template>
  <div class="modal">
    <div class="sa-icon sa-info"></div>
    <h2 class="modal__title">Начать игру!</h2>
    <p class="modal__text">Выберите свой уровень сложности.</p>
    <div class="container__btn">
      <button class="btn__normal" @click="speedSave(1500)">Нормальный</button>
      <button class="btn__normal btn__normal-sr" @click="speedSave(1000)">Средний</button>
      <button class="btn__normal btn__normal-hr" @click="speedSave(400)">Сложный</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'StartPopup',
  methods: {
    speedSave(item) {
      this.$emit('speed-saveGame', item);
    },
  },
};
</script>

<style scoped lang="scss">
  @import '../assets/style/StartPopup.sass';
</style>