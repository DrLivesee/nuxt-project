<template>
  <form @submit.prevent="submitForm" class="form">
    <div class="form__row">
      <div
        :class="[
          'form__input-container',
          'form__input-container--number',
          { 'form__input--error': errors.carNumber },
        ]"
      >
        <label for="car-number" class="form__label">Номер автомобиля</label>
        <input
          id="car-number"
          v-model="carNumber"
          class="form__input"
          @focus="clearError('carNumber')"
        />
      </div>

      <div
        :class="[
          'form__input-container',
          'form__input-container--region',
          { 'form__input--error': errors.region },
        ]"
      >
        <label for="car-region" class="form__label">Регион</label>
        <input
          id="car-region"
          v-model="region"
          class="form__input"
          @focus="clearError('region')"
        />
      </div>
    </div>
    <div
      :class="[
        'form__input-container',
        { 'form__input--error': errors.registration },
      ]"
    >
      <label for="car-registration" class="form__label"
        >Свидетельство о регистрации ТС</label
      >
      <input
        id="car-registration"
        v-model="registration"
        class="form__input"
        @focus="clearError('registration')"
      />
    </div>
    <div class="form__actions">
      <button type="submit" class="form__button form__button--fines">
        <span>Проверить штрафы</span><img src="/img/arrow.svg" />
      </button>
      <button
        @click="showModal"
        type="button"
        class="form__button form__button--service"
      >
        <img src="/img/youtube.svg" /><span class="form__button--text"
          >О сервисе</span
        ><span class="form__button--time">(1 мин. 20 сек)</span>
      </button>
    </div>
    <p class="form__text">
      Нажимая «Проверить штрафы» вы соглашаетесь с политикой обработки
      персональных данных и принимаете оферту
    </p>
  </form>
</template>

<script setup>
import { ref } from "vue";

const emits = defineEmits(["showModal"]);

const showModal = () => {
  emits("showModal");
};

const carNumber = ref("");
const region = ref("");
const registration = ref("");
const errors = ref({
  carNumber: false,
  region: false,
  registration: false,
});

const clearError = (field) => {
  errors.value[field] = false;
};

function submitForm() {
  errors.value.carNumber = !carNumber.value;
  errors.value.region = !region.value;
  errors.value.registration = !registration.value;

  if (!carNumber.value || !region.value || !registration.value) {
    alert("Заполните все поля");
    return;
  }

  alert("Данные отправлены");
  carNumber.value = ''
  region.value = ''
  registration.value = ''
}
</script>

<style lang="scss" scoped>
.form {
  display: flex;
  flex-direction: column;
  gap: 16px;

  &__row {
    display: flex;
    gap: 30px;

    @media (max-width: 768px) {
      flex-direction: column;
      gap: 16px;
    }
  }

  &__input-container {
    display: flex;
    flex-direction: column;
    gap: 5px;
    width: 100%;

    &--number {
      width: 100%;
    }

    &--region {
      width: 100%;
      max-width: 213px;

      @media (max-width: 768px) {
        max-width: 100%;
      }
    }
  }
  &__input--error {
    .form__input {
      border-color: red;
    }
  }

  &__label {
    font-size: 12px;
    line-height: 120%;
  }

  &__input {
    padding: 10px;
    border: 1px solid #bcbcbc;
    flex: 1;
    outline: none;
    border-radius: 5px;

    &:focus {
      border-color: #0584fe;
    }
  }

  &__actions {
    display: flex;
    gap: 21px;

    @media (max-width: 768px) {
      flex-direction: column;
      gap: 16px;
    }

    .form__button {
      @media (min-width: 769px) and (max-width: 1060px) {
        padding: 8px 6px;
        font-size: 14px;
        gap: 2px;
      }
    }
  }

  &__button {
    display: flex;
    align-items: center;
    gap: 4px;
    padding: 11px 20px;
    font-size: 18px;
    background-color: #0584fe;
    color: white;
    border: none;
    cursor: pointer;
    border-radius: 7px;
    transition: background-color 0.3s;

    &:hover {
      background-color: #0056b3;
    }

    &--fines img {
      padding-top: 3px;
    }

    &--service {
      background-color: transparent;
      color: #0584fe;
      border: 1px solid #0584fe;

      &:hover {
        background-color: #e6f2ff;
      }
    }

    &--text {
      color: black;
    }

    &--time {
      font-size: 15px;
      color: #1253a2;
    }
  }

  &__text {
    font-size: 13px;
    color: #8f8f8f;
    line-height: 120%;
  }
}
</style>
