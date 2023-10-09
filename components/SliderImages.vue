<template>
  <div class="slider" ref="slider">
    <div class="slider__slides">
      <div
        class="slider__slide"
        v-for="(slide, index) in props.images"
        :key="slide"
        :id="`slide-${index}`"
      >
        <img :src="slide" alt="product" />
      </div>
    </div>
    <div class="slider__nav">
      <button
        v-for="(img, index) in props.images"
        :key="img"
        @click="toggleSlide(index)"
        :class="{ active: index === state.currentSliderIndex }"
      />
    </div>
  </div>
</template>

<script setup lang="ts">
import { onMounted, reactive, ref } from "vue";
const props = defineProps<{
  images: string[];
}>();

const slider = ref<HTMLInputElement | null>(null)
const state = reactive({
  currentSliderIndex: 0,
});
onMounted(() => {
  console.log(slider);
});

function toggleSlide(index: number) {
  const container = slider.value!.children[0];
  const slideWidth = document.getElementById("slide-0")!.offsetWidth;
  // 10 is 10px gap between slides
  const scroll = !index ? 0 : slideWidth * index + 10 * index;
  container.scrollTo({
    left: scroll,
    behavior: "smooth",
  });

  state.currentSliderIndex = index;
}
</script>

<style lang="scss">
@import "styles/variables";

.slider {
  &__slides {
    display: flex;
    gap: 10px;
    overflow-x: auto;
    overflow-y: hidden;
  }
  &__slide {
    flex-shrink: 0;
    // 80px is left, right page paddings
    // 50px next img preview = 160px
    width: calc(100vw - 130px);
    box-sizing: border-box;
    aspect-ratio: 6/5;
    img {
      width: 100%;
      height: 100%;
    }
  }
  &__nav {
    margin-top: 18px;
    display: flex;
    gap: 20px;
    button {
      height: 30px;
      width: 30px;
      background-color: #adc2bd;
      border-radius: 50%;
      cursor: pointer;
      &.active {
        background-color: $c-main;
      }
    }
  }
  @include mobile {
    &__slide {
      // 40px is left, right page paddings
      // 30px next img preview = 160px
      width: calc(100vw - 70px);
    }
    &__nav {
      button {
        height: 10px;
        width: 10px;
      }
    }
  }
}
</style>
