<script setup lang="ts">
import { computed, reactive } from "vue";
import StarsRating from "@/components/StarsRating.vue";
import DynamicPrice from "@/components/DynamicPrice.vue";
import ValuesList from "@/components/ValuesList.vue";
import SliderImages from "@/components/SliderImages.vue";
import p1 from '@/assets/images/product/1.png'
import p2 from '@/assets/images/product/2.png'
import p3 from '@/assets/images/product/3.png'
import p4 from '@/assets/images/product/4.png'
const images = [p1, p2, p3, p4];
const sizesMan = [7, 8, 9, 10, 11, 12, 13, 14, 15];
const sizesWoman = [5, 6, 7, 8, 9, 10, 11, 12];

const state = reactive({
  isGenderMen: true,
  currentSize: 10,
  isWidthStandard: true,
  prevWomanSize: 7,
  prevManSize: 10,
});

const currentSizeGender = computed(() => {
  return state.isGenderMen ? sizesMan : sizesWoman;
});

function toggleGender() {
  if (state.isGenderMen) {
    state.prevManSize = state.currentSize;
  } else {
    state.prevWomanSize = state.currentSize;
  }
  state.isGenderMen = !state.isGenderMen;
  state.currentSize = state.isGenderMen
      ? state.prevManSize
      : state.prevWomanSize;
}
</script>

<template>
  <main class="product">
    <div class="product__images">
      <img :src="img" alt="product" v-for="img in images" />
    </div>
    <slider-images :images="images" />
    <div class="product__content">
      <h1 class="product__title">The Classic Insole</h1>
      <div class="product__reviews">
        <stars-rating value="5"></stars-rating>
        <a href="#">150 Reviews</a>
      </div>
      <DynamicPrice old-price="60" new-price="48" />
      <p class="product__description">
        All day comfort and support unique to your body. Great for:
      </p>
      <values-list
          :included="['Foot pain', 'Knee pain']"
          :excluded="['Back pain', 'Alignment']"
      />
      <p class="product__label">Width:</p>
      <div class="product__bool-buttons">
        <button
            class="product__btn"
            :class="{ 'product__btn--active': state.isWidthStandard }"
            @click="state.isWidthStandard = true"
        >
          Standard
        </button>
        <button
            class="product__btn"
            :class="{ 'product__btn--active': !state.isWidthStandard }"
            @click="state.isWidthStandard = false"
        >
          Narrow
        </button>
      </div>
      <p class="product__label">Gender:</p>
      <div class="product__bool-buttons">
        <button
            class="product__btn"
            :class="{ 'product__btn--active': state.isGenderMen }"
            @click="toggleGender"
        >
          Men
        </button>
        <button
            class="product__btn"
            :class="{ 'product__btn--active': !state.isGenderMen }"
            @click="toggleGender"
        >
          Women
        </button>
      </div>
      <p class="product__label product__label--help">
        <span>Size:</span>
        <a href="#">help me choose</a>
      </p>
      <div class="product__sizes">
        <button
            class="product__btn"
            v-for="size in currentSizeGender"
            :class="{ 'product__btn--active': size === state.currentSize }"
            @click="state.currentSize = size"
        >
          {{ size }}
        </button>
      </div>
      <button class="product__add"><span>Add to Cart</span> $48</button>
      <div class="product__comfort">
        <img src="~/assets/images/book.png" alt="" />
        90-day comfort guarantee
      </div>
    </div>
  </main>
</template>

<style lang="scss">
@import "styles/variables";
.product {
  @include max-width();
  margin-top: 55px;
  display: grid;
  grid-template-columns: 1fr 375px;
  grid-gap: 30px;

  &__images {
    display: grid;
    grid-template-columns: 1fr 1fr;
    justify-content: center;
    grid-column-gap: 22px;
    grid-row-gap: 47px;
    img {
      border-radius: 20px;
      width: 100%;
      height: 100%;
      object-fit: cover;
    }
  }
  &__title {
    font-size: 30px;
    text-transform: capitalize;
  }
  &__reviews {
    margin-top: 5px;
    display: flex;
    align-items: center;
    gap: 5px;
    a {
      font-size: 15px;
      color: black;
      text-decoration: underline;
    }
  }
  &__description {
    font-size: 18px;
    margin-top: 30px;
  }
  &__label {
    margin-top: 10px;
    font-size: 14px;
    &--help {
      display: flex;
      justify-content: space-between;
      gap: 10px;
      a {
        text-decoration: underline;
      }
    }
  }
  &__btn {
    border: solid 1px $c-main;
    border-radius: 10px;
    font-size: 18px;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 8px 13px;
    &--active {
      background-color: $c-main;
      color: $c-accent;
    }
  }
  &__bool-buttons {
    margin-top: 5px;
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 10px;
  }
  &__sizes {
    margin-top: 5px;
    display: flex;
    flex-wrap: wrap;
    gap: 14px;
    justify-content: center;
  }
  &__add {
    margin-top: 20px;
    display: block;
    width: 100%;
    padding: 15px;
    color: white;
    background-color: $c-main;
    span {
      margin-right: 15px;
    }
  }
  &__comfort {
    margin-top: 20px;
    display: flex;
    justify-content: center;
    gap: 10px;
    font-size: 22px;
    img {
      height: 25px;
    }
  }
  .slider {
    display: none;
  }
  .values {
    margin-top: 20px;
  }
  @media screen and (max-width: 1200px) {
    margin-top: 30px;
    grid-template-columns: 1fr;
    grid-gap: 30px;
    display: block;
    &__content {
      margin-top: 30px;
    }
    &__bool-buttons {
      grid-template-columns: 150px 150px;
      justify-content: center;
    }
  }
  @include tablet {
    &__images {
      display: none;
    }
    .slider {
      display: block;
    }
  }
}
</style>
