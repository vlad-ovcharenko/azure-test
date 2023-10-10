<template>
  <div class="stars">
    <label
      v-for="rating in maxRating"
      :key="rating"
      class="stars__star"
      :class="{
        'stars__star--selected': getSelectedStatus(rating),
        'stars__star--disabled': props.disabled,
      }"
      @click="setRating(rating)"
      @mouseover="starOver(rating)"
      @mouseout="starOut"
    >
      <input
        class="stars__checkbox"
        type="radio"
        :value="rating"
        :disabled="props.disabled"
      />★
    </label>
  </div>
</template>

<script setup lang="ts">
import { reactive } from "vue";
const maxRating = 5;

const props = defineProps<{
  value: number;
  disabled?: boolean;
}>();
const state = reactive(<
  {
    value: number;
    tempValue: number | null;
  }
>{
  value: props.value,
  tempValue: null,
});
function getSelectedStatus(rating: number) {
  if (state.tempValue) {
    return state.tempValue >= rating;
  }
  return state.value >= rating;
}
function setRating(rating: number) {
  if (!props.disabled) {
    state.value = rating;
  }
}
function starOver(rating: number) {
  if (!props.disabled) {
    state.tempValue = rating;
  }
}
function starOut() {
  if (!props.disabled) {
    state.tempValue = null;
  }
}
</script>

<style lang="scss">
@import "styles/variables";
.stars {
  display: flex;
  &__star {
    display: inline-block;
    vertical-align: middle;
    line-height: 1;
    font-size: 18px;
    color: #ababab;
    transition: color 0.2s ease-out;

    &:hover {
      cursor: pointer;
    }

    &--selected {
      color: $c-accent;
    }

    &--disabled:hover {
      cursor: not-allowed;
    }
  }

  &__checkbox {
    position: absolute;
    overflow: hidden;
    clip: rect(0 0 0 0);
    height: 1px;
    width: 1px;
    margin: -1px;
    padding: 0;
    border: 0;
  }
}
</style>
