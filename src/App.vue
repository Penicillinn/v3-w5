<template>
  <div class="root">
    <h1>{{ a }}</h1>
    <h1>doubleA --- {{ doubleA }}</h1>
    <button @click="test">ceshi yixia </button>
  </div>
</template>

<script>
import { computed, ref } from 'vue';
export default {
  setup() {
    const a = ref(3);
    const test = () => {
      a.value = a.value + 1;
    };
    const doubleA = computed(() => a.value * 2)
    return {
      test,
      a,
      doubleA
    }
  }
}
</script>
<style scoped>
</style>