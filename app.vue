<template>
  <Header v-if="isAuth" />
  <NuxtPage />
</template>

<script setup>
const route = useRoute();

const isAuth = computed(() => !['/login', '/registration'].includes(route.fullPath));
</script>

<style lang="scss">
@import "/assets/scss/main.scss";
@import url("https://fonts.googleapis.com/css2?family=PT+Sans:wght@400;700&display=swap");
</style>