<template>
  <div class="main-container">
    <nav class="breadcrumbs">
      <router-link to="/">Главная страница</router-link>
      <span class="breadcrumbs__separator"> <div class="breadcrumbs__circle"></div> </span>
      <router-link to="/documents">Документы</router-link>
      <span class="breadcrumbs__separator"> <div class="breadcrumbs__circle"></div> </span>
      <span class="breadcrumbs__separator--active">{{ document.title }}</span>
    </nav>
    <div class="document">
      <h1 class="document__title">{{ document.title }}</h1>
      <div
        v-for="content in document.content"
        :key="content.id"
        class="document__content"
      >
        <h2 class="document__content-title">{{ content.title }}</h2>
        <p
          class="document__content-description"
          v-html="content.description"
        ></p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import { useRoute } from "vue-router";
import axios from "axios";

const route = useRoute();
const document = ref({ title: "", content: [] });

const fetchDocument = async () => {
  try {
    const resp = await axios.get("/api/documents.json");

    const doc = resp.data.find((d) => d.id == route.params.id);
    if (doc) {
      document.value = doc;
    } else {
      console.error("Document not found");
    }
  } catch (error) {
    console.error("Error fetching document:", error);
  }
};

onMounted(() => {
  fetchDocument();
});
</script>

<style lang="scss" scoped>
.breadcrumbs {
  font-size: 14px;
  margin-bottom: 20px;
  padding-top: 20px;
  display: flex;
  align-items: center;
  gap: 10px;

  a {
    font-size: 13px;
    line-height: 120%;
    color: #000000;
    text-decoration: none;

    @media (max-width: 768px) {
      font-size: 12px;
      
  }

    &:hover {
      text-decoration: underline;
    }
  }

  &__circle {
    width: 5px;
    height: 5px;
    background-color: #000000;
    border-radius: 50px;
  }

  &__separator {
    margin: 0 5px;
  }

  &__separator--active {
    color: #8F8F8F;
  }
}
.document {
  &__title {
    font-size: 41px;
    line-height: 120%;
    margin-bottom: 40px;
    color: #000000;

    @media (max-width: 768px) {
      font-size: 32px;
      margin-bottom: 24px;
  }
  }

  &__content {
    margin-bottom: 30px;

    &-title {
      font-size: 41px;
      margin-bottom: 25px;
      color: #383838;

      @media (max-width: 768px) {
      font-size: 32px;
      margin-bottom: 15px;
  }
    }

    &-description {
      font-size: 18px;
      line-height: 120%;
      color: #000000;

      @media (max-width: 768px) {
      font-size: 16px;
      
  }
    }
  }
}
</style>
