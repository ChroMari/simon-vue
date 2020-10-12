<template>
  <div class="modal">
    <div class="sa-icon sa-info">
      <span class="sa-line sa-left"></span>
      <span class="sa-line sa-right"></span>
    </div>
    <h2 class="modal__title">Увы, Вы проиграли!</h2>
    <p class="modal__text">Попробуйте сыграть снова.</p>
  </div>
</template>

<script>
export default {
  name: 'FailPopup',
};
</script>

<style scoped lang="scss">
  @import '../assets/style/FailPopup.sass';
</style>