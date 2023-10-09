<template>
  <div class="values">
    <ul class="values__included">
      <li v-for="str in props.included">{{ str }}</li>
    </ul>
    <ul class="values__not-included" v-if="props.excluded">
      <li v-for="str in props.excluded">
        {{ str }}
      </li>
    </ul>
  </div>
</template>

<script setup lang="ts">
const props = defineProps<{
  included: string[];
  excluded: string[];
}>();
</script>

<style lang="scss">
@import "styles/variables";
.values {
  display: grid;
  grid-template-columns: auto auto;
  grid-column-gap: 40px;
  justify-content: start;
  li {
    margin-left: 15px;
  }
  &__not-included {
    color: rgba($c-main, 0.6);
  }
}
</style>
