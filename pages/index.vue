<template>
  <div class="main-container">
    <main>
      <section class="hero">
        <div class="hero__content">
          <h1 class="hero__title">Проверьте штрафы и зарегистрируйтесь в 1 клик</h1>
          <Form @showModal="showModal" />
        </div>
        <div class="hero__image">
          <img src="/img/hero.png" alt="Devices showing the service" />
        </div>
      </section>

      <section class="benefits">
        <div class="benefits__content">
          <h1 class="benefits__title">Плюсы использования сервиса «Компас» для анализа штрафов</h1>
          <Benefits />
        </div>
      </section>

      <section class="documents">
        <div class="documents__content">
          <h1 class="documents__title">Документы</h1>
          <DocumentsSlider />
        </div>
      </section>
    </main>
    <Modal v-if="isShowModal" @closeModal="closeModal" />
  </div>
</template>

<script setup>
const isShowModal = ref(false);

const showModal = () => {
  isShowModal.value = true;
};

const closeModal = () => {
  isShowModal.value = false;
};
</script>

<style lang="scss" scoped>
.hero {
  display: flex;
  justify-content: space-between;
  gap: 40px;
  align-items: center;
  padding: 89px 0 48px;

  @media (max-width: 768px) {
    flex-direction: column;
    padding: 32px 0 41px;
  }

  &__title {
    font-size: 41px;
    font-weight: bold;
    margin-bottom: 25px;
    line-height: 120%;

    @media (max-width: 768px) {
      font-size: 32px;
    }
  }

  &__content {
    flex: 1;
  }

  &__image {
    flex: 1;

    img {
      max-width: 100%;
    }
  }
}

.benefits {
  padding: 50px 0 40px;

  @media (max-width: 768px) {
    padding: 20px 0 20px;
  }

  &__content {
    flex: 1;
  }

  &__title {
    font-size: 32px;
    font-weight: bold;
    margin-bottom: 33px;
    text-align: center;
    line-height: 120%;

    @media (max-width: 768px) {
      text-align: start;
    }
  }
}

.documents {
  padding: 35px 0 40px;

  @media (max-width: 768px) {
    padding: 20px 0 20px;
  }

  &__content {
    flex: 1;
  }

  &__title {
    font-size: 32px;
    font-weight: bold;
    margin-bottom: 20px;
    text-align: center;
    line-height: 120%;

    @media (max-width: 768px) {
      text-align: start;
    }
  }
}
</style>