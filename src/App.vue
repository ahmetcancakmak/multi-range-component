<template>
  <div class="h-screen flex justify-center items-center">
    <div class="relative max-w-xl w-full">
      <div>
        <MultiRangeComponent
          :min="min"
          :max="max"
          :step="step"
          v-model:label="label"
        />
        <div class="flex justify-between items-center py-5">
          <div>
            <input
              type="text"
              v-model="label[0]"
              class="px-3 py-2 border border-gray-200 rounded w-24 text-center"
            />
          </div>
          <div>
            <input
              type="text"
              v-model="label[1]"
              class="px-3 py-2 border border-gray-200 rounded w-24 text-center"
            />
          </div>
        </div>
      </div>
    </div>
  </div>
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
      min: 0,
      max: 1000,
      step: 0.1,
      label: [0, 1],
    };
  },
};
</script>

<style>
</style>
