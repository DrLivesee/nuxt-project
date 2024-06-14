<template>
  <header class="header">
    <div class="header__content">
      <div class="header__navigation-container">
        <div class="header__logo">
          <img src="/img/logo.svg" alt="COMPAS" @click="redirectToHome" />
        </div>
        <nav class="header__nav">
          <router-link to="/tariffs" class="header__link">Тарифы</router-link>
          <router-link to="/contacts" class="header__link"
            >Контакты</router-link
          >
        </nav>
      </div>
      <div class="header__contact">
        <span class="header__phone">+7 495 118-44-22</span>

        <div class="header__auth">
          <router-link to="/login" class="header__link header__link-login"
            >Вход</router-link
          >
          <router-link to="/registration" class="header__register-button">Регистрация</router-link>
        </div>
      </div>
    </div>
  </header>
</template>

<script setup>
const router = useRouter();

function redirectToHome() {
  router.push("/");
}

</script>

<style lang="scss" scoped>
.header {
  display: flex;
  justify-content: center;
  padding: 12px 15px;
  padding-bottom: 11px;
  background: linear-gradient(
    90deg,
    rgba(0, 0, 0, 1) 30%,
    rgba(28, 39, 52, 1) 73%
  );
  color: #fff;

  &__navigation-container {
    display: flex;
    gap: 31px;

    @media (max-width: 768px) {
      flex-direction: column;
      align-items: flex-start;
      width: 100%;
      gap: 10px;
    }
  }

  &__content {
    width: 100%;
    max-width: 1156px;
    display: flex;
    justify-content: space-between;
    align-items: center;

    @media (max-width: 768px) {
      flex-direction: column;
      align-items: flex-start;
    }
  }

  &__logo img {
    cursor: pointer;

    @media (max-width: 768px) {
      margin-bottom: 1rem;
    }
  }

  &__nav {
    display: flex;
    gap: 30px;

    @media (max-width: 768px) {
      display: block;
      width: 100%;
      padding-bottom: 20px;

      .header__link {
        padding-right: 20px;
        
      }
    }
  }

  &__link {
    color: #fff;
    text-decoration: none;
    transition: color 0.3s;
    font-size: 18px;

    &:hover {
      color: #0584FE;
    }

    @media (max-width: 768px) {
      width: 100%;
      text-align: left;
    }
  }

  &__contact {
    display: flex;
    align-items: center;
    gap: 30px;

    @media (max-width: 768px) {
      flex-direction: column;
      align-items: flex-start;
      width: 100%;
      gap: 20px;
    }

    .header__auth {
      display: flex;
      align-items: center;
      gap: 30px;
      @media (max-width: 768px) {
        width: 100%;
      }

      .header__link-login {
        padding: 7px 0px;
      }
    }
  }

  &__phone {
    font-size: 18px;
    font-weight: bold;
  }

  &__register-button {
    text-decoration: none;
    background-color: #0584FE;
    color: #fff;
    border: none;
    padding: 9px 18px;
    cursor: pointer;
    border-radius: 7px;
    transition: background-color 0.3s;
    font-size: 15px;

    &:hover {
      background-color: #0056b3;
    }

    @media (max-width: 768px) {
      width: 100%;
      text-align: center;
    }
  }
}
</style>
