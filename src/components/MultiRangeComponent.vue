<template>
  <input
    type="range"
    :step="step"
    :min="min"
    :max="max"
    :change="minLimitSetter()"
    v-model="rangeValue[0]"
    class="
      absolute
      pointer-events-none
      appearance-none
      z-20
      h-2
      w-full
      opacity-0
      cursor-pointer
    "
  />
  <input
    type="range"
    :step="step"
    :min="min"
    :max="max"
    :change="maxLimitSetter()"
    v-model="rangeValue[1]"
    class="
      absolute
      pointer-events-none
      appearance-none
      z-20
      h-2
      w-full
      opacity-0
      cursor-pointer
    "
  />
  <div class="relative z-10 h-2">
    <div
      class="absolute z-10 left-0 right-0 bottom-0 top-0 rounded-md bg-gray-200"
    ></div>
    <div
      class="absolute z-20 top-0 bottom-0 rounded-md bg-green-300"
      :style="'right:' + rangeThumb[1] + '%; left:' + rangeThumb[0] + '%'"
    ></div>
    <div
      class="
        absolute
        z-30
        w-6
        h-6
        top-0
        left-0
        bg-green-300
        rounded-full
        -mt-2
        -ml-1
      "
      :style="'left: ' + rangeThumb[0] + '%'"
    ></div>
    <div
      class="
        absolute
        z-30
        w-6
        h-6
        top-0
        right-0
        bg-green-300
        rounded-full
        -mt-2
        -mr-3
      "
      :style="'right: ' + rangeThumb[1] + '%'"
    ></div>
  </div>
</template>

<script>
export default {
  name: "MutliRangeComponent",
  props: {
    min: Number,
    max: Number,
    step: Number,
    label: Array,
  },
  emits: ["update:label"],
  data() {
    return {
      rangeValue: new Array(),
      rangeThumb: [0, 0],
    };
  },
  methods: {
    minLimitSetter() {
      if (((this.rangeValue[0] - this.min) / (this.max - this.min)) * 100 > 0) {
        this.rangeValue[0] = Math.min(
          this.rangeValue[0],
          this.rangeValue[1] - this.step
        );
        this.rangeThumb[0] =
          ((this.rangeValue[0] - this.min) / (this.max - this.min)) * 100;
      } else {
        this.rangeThumb[0] = 0;
      }
      this.$emit("update:label", this.rangeValue);
    },
    maxLimitSetter() {
      this.rangeValue[1] = Math.max(
        this.rangeValue[1],
        this.rangeValue[0] + this.step
      );
      this.rangeThumb[1] =
        100 - ((this.rangeValue[1] - this.min) / (this.max - this.min)) * 100;
      this.$emit("update:label", this.rangeValue);
    },
  },
  created() {
    this.rangeValue[0] = this.min;
    this.rangeValue[1] = this.max;
  },
};
</script>

<style scoped>
input[type="range"]::-webkit-slider-thumb {
  pointer-events: all;
  width: 24px;
  height: 24px;
  -webkit-appearance: none;
}
</style>