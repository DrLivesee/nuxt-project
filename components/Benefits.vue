<template>
  <section class="benefits">
    <div
      class="benefits__item"
      v-for="benefit in benefits"
      :key="benefit.title"
    >
      <img :src="`/img/${benefit.img}.svg`" class="benefits__item-image" />
      <div class="benefits__item-text">
        <h3 class="benefits__item-title">{{ benefit.title }}</h3>
        <p class="benefits__item-description">{{ benefit.description }}</p>
      </div>
    </div>
  </section>
</template>

<script setup>
const benefits = [
  {
    img: "car-park",
    title: "Неограниченный автопарк",
    description: "Можно добавлять неограниченное количество машин и водителей.",
  },
  {
    img: "expenses",
    title: "Сокращение затрат",
    description:
      "Максимально быстро узнаете о штрафах в автоматическом режиме, тем самым у вас есть время оплатить по скидке",
  },
  {
    img: "safety",
    title: "Безопасность",
    description:
      "Данные передаются в зашифрованном виде, они доступны только получателю",
  },
  {
    img: "repayment",
    title: "Уведомление о погашении",
    description:
      "Мы оповестим вас о том, что штраф был погашен и соответствующая запись создана в ГИС ГМП",
  },
  {
    img: "receipt",
    title: "Квитанция об оплате",
    description:
      "После совершения оплаты банковской картой на вашу электронную почту придет квитанция об успешной оплате.",
  },
  {
    img: "story",
    title: "Вся история сохраняется",
    description:
      "Вся история штрафов сохраняется по машине и водителю, позволяет анализировать статистику по штрафам.",
  },
];
</script>

<style lang="scss" scoped>
.benefits {
  display: flex;
  flex-wrap: wrap;
  gap: 35px;
  justify-content: space-between;

  @media (min-width: 769px) and (max-width: 1185px) {
    gap: 15px;
  }

  @media (max-width: 768px) {
    flex-direction: column;
    gap: 20px;
  }

  &__item {
    display: flex;
    align-items: center;
    background-color: #fbfcfd;
    padding: 24px 20px;
    border: 1px solid #eeeff1;
    text-align: center;
    border-radius: 10px;
    width: 100%;
    max-width: 362px;
    gap: 16px;
    flex-grow: 1;

    &:nth-child(3),
    &:nth-child(5)  {
      gap: 22px;
    }

    @media (min-width: 769px) and (max-width: 1185px) {
      width: 40%;
      max-width: none;
    }

    @media (max-width: 768px) {
      max-width: none;
    }

    &:nth-child(3) .benefits__item-image,
    &:nth-child(5) .benefits__item-image {
      max-width: 53px;
    }
  }

  &__item-image {
    width: 100%;
    max-width: 59px;
  }

  &__item-text {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    gap: 10px;
  }

  &__item-title {
    color: #1253a2;
    font-size: 18px;
    font-weight: bold;
    text-align: start;
    line-height: 120%;
  }

  &__item-description {
    font-size: 15px;
    color: #000000;
    text-align: start;
    line-height: 120%;
  }
}
</style>