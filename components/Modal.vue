<template>
  <div class="modal" @click.self="closeModal">
    <div class="modal__content">
      <button class="modal__close" @click="closeModal">
        <img src="/img/close.svg" alt="close" />
      </button>
      <iframe
        class="modal__video"
        src="https://www.youtube.com/embed/dQw4w9WgXcQ"
        frameborder="0"
        allowfullscreen
      ></iframe>
    </div>
  </div>
</template>

<script setup>
const emits = defineEmits(["closeModal"]);

const closeModal = () => {
  emits("closeModal");
};
</script>

<style lang="scss" scoped>
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.8);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;

  &__content {
    background-color: #000000;
    position: relative;
    width: 100%;
    max-width: 960px;
    height: 100%;
    max-height: 532px;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  &__close {
    position: absolute;
    top: -50px;
    right: 0;
    background: none;
    border: none;
    font-size: 2rem;
    color: #fff;
    cursor: pointer;
  }

  &__video {
    width: 100%;
    height: 100%;
  }
}
</style>