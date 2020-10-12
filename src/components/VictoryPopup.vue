<template>
  <div class="modal">
   <div class="sa-icon sa-success">
      <span class="sa-line sa-tip"></span>
      <span class="sa-line sa-long"></span>
    </div>
    <h2 class="modal__title">Вы выиграли!</h2>
    <p class="modal__text">Попробуйте теперь сыграть на более сложном уроне.</p>
  </div>
</template>

<script>
export default {
  name: 'VictoryPopup',
};
</script>

<style scoped lang="scss">
  @import '../assets/style/VictoryPopup.sass';
</style>