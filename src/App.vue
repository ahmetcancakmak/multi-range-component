<template>
  <MultiRangeComponent :min="min" :max="max" :step="step"/>
</template>

<script>
import MultiRangeComponent from "./components/MultiRangeComponent.vue";

export default {
  name: "App",
  components: {
    MultiRangeComponent,
  },
  data() {
    return {
      min:0,
      max:1,
      step:0.1
    }
  }
};
</script>

<style>
</style>
