<template>
  <section class="documents">
    <swiper
      :modules="modules"
      :slides-per-view="slidesPerView"
      :pagination="{ clickable: true }"
      :navigation="{
        nextEl: '.swiper-button-next',
        prevEl: '.swiper-button-prev',
      }"
      :space-between="spaceBetween"
      :loop="false"
      class="documents__swiper"
    >
      <swiper-slide v-for="doc in documents" :key="doc.id">
        <div class="documents__card">
          <div class="documents__text">
            <h3 class="documents__title">{{ doc.title }}</h3>
            <p class="documents__description">{{ doc.description }}</p>
          </div>
          <router-link :to="`/documents/${doc.id}`" class="documents__link"
            >Перейти</router-link
          >
        </div>
      </swiper-slide>
      <img
        :src="arrowLeftNavigation"
        alt="arrow"
        class="swiper-button-prev custom-swiper-button-prev"
      />
      <img
        :src="arrowRightNavigation"
        alt="arrow"
        class="swiper-button-next custom-swiper-button-next"
      />
    </swiper>
  </section>
</template>

<script setup>
import { Swiper, SwiperSlide } from "swiper/vue";
import { Navigation, Pagination } from "swiper/modules";
import "swiper/swiper-bundle.css";
import axios from "axios";

const arrowLeftNavigation = ref("/img/arrow-left-nav.svg");
const arrowRightNavigation = ref("/img/arrow-right-nav.svg");

const documents = ref([]);

const fetchDocuments = async () => {
  try {
    const resp = await axios.get("/api/documents.json");
    documents.value = resp.data;
  } catch (error) {
    console.error("Error fetching documents:", error);
  }
};

onMounted(async () => {
  await fetchDocuments();
});

const modules = [Navigation, Pagination];

const windowWidth = ref(1024);

const slidesPerView = computed(() => (windowWidth.value < 768 ? 1 : 3));
const spaceBetween = computed(() => (windowWidth.value < 1060 ? 20 : 35));

const updateWidth = () => {
  if (typeof window !== "undefined") {
    windowWidth.value = window.innerWidth;
  }
};

onMounted(() => {
  if (typeof window !== "undefined") {
    window.addEventListener("resize", updateWidth);
    updateWidth();
  }
});

onUnmounted(() => {
  if (typeof window !== "undefined") {
    window.removeEventListener("resize", updateWidth);
  }
});
</script>

<style lang="scss" scoped>
.documents {
  &__swiper-container {
    overflow: hidden;
    position: relative;
  }
  &__swiper {
    padding: 20px 30px;

    @media (max-width: 1060px) {
      padding: 20px;
    }

    :deep(.custom-swiper-button-prev),
    :deep(.custom-swiper-button-next) {
      display: block;
      position: absolute;
      top: calc(50% - 40px);
      width: 40px;
      height: 80px;
      background-size: contain;
      background-repeat: no-repeat;
      z-index: 10;
      cursor: pointer;

      &::before {
        content: "";
      }
    }

    :deep(.custom-swiper-button-prev) {
      left: 0px;
    }

    :deep(.custom-swiper-button-next) {
      right: 0px;
    }

    :deep(.swiper-pagination) {
      position: absolute;
      bottom: 0px;
      display: flex;
      justify-content: center;
      align-items: center;
    }

    :deep(.swiper-pagination-bullet) {
      opacity: 1;
      background-color: #d9d9d9;
      width: 7px;
      height: 7px;
    }

    :deep(.swiper-pagination-bullet-active) {
      background-color: #007aff;
      width: 10px;
      height: 10px;
    }
  }

  &__card {
    box-shadow: none;
    border: 1px solid #eeeff1;
    background-color: #fff;
    border-radius: 10px;
    padding: 25px;
    width: 100%;
    max-width: 340px;
    min-height: 450px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;

    @media (min-width: 769px) and (max-width: 1060px) {
      max-width: none;
    }

    @media (max-width: 768px) {
      max-width: none;
      min-height: 350px;
    }
  }

  :deep(.swiper-slide-active),
  :deep(.swiper-slide-next),
  :deep(.swiper-slide-next + .swiper-slide) {
    .documents__card {
      box-shadow: 0px 0px 20px 0px rgba(0, 0, 0, 0.12);
    }
  }

  @media (max-width: 768px) {
    :deep(.swiper-slide-next),
    :deep(.swiper-slide-next + .swiper-slide) {
      .documents__card {
        box-shadow: none;
      }
    }
  }

  &__title {
    font-size: 31px;
    font-weight: bold;
    color: #1253a2;
    margin-bottom: 15px;
    line-height: 120%;

    @media (max-width: 1060px) {
      font-size: 24px;
    }
    @media (min-width: 481px) and (max-width: 768px) {
      font-size: 28px;
    }
  }

  &__description {
    font-size: 18px;
    line-height: 120%;
  }

  &__link {
    text-align: center;
    text-decoration: none;
    background-color: #0584fe;
    color: #fff;
    border: none;
    padding: 11px 0px;
    cursor: pointer;
    border-radius: 7px;
    transition: background-color 0.3s;
    font-size: 18px;
    width: 100%;

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
