<template>
  <div class="price">
    <span class="price__new">{{ props.newPrice }}$</span>
    <span v-if="props.oldPrice" class="price__old">{{ props.oldPrice }}$</span>
    <div v-if="props.oldPrice" class="price__off">{{ getPercent() }}% OFF</div>
  </div>
</template>

<script setup lang="ts">
const props = defineProps<{
  newPrice: number
  oldPrice?: number
}>()
function getPercent() {
  const saving = props.oldPrice! - props.newPrice
  const savingPercent = (saving / props.oldPrice!) * 100
  return savingPercent.toFixed(2)
}
</script>

<style lang="scss">
@import 'styles/variables';
.price {
  display: flex;
  align-items: center;
  margin-top: 15px;
  font-size: 30px;
  gap: 15px;
  &__old {
    color: rgba($c-main, 0.6);
    text-decoration: line-through;
  }
  &__off {
    background-color: #adc2bd;
    font-size: 20px;
    padding: 10px 10px;
  }
}
</style>
