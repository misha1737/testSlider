<template>
  <div class="slider">
    <h1>Slider</h1>
    <div id="slider" ref="slider"></div>
    <div class="transactionValue">
      <input
        id="slider-input"
        v-model.lazy="value"
        v-on:change="updateSlider"
      />
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import noUiSlider from "nouislider";
import "nouislider/distribute/nouislider.css";
import { nextTick } from "vue/types/umd";
export default Vue.extend({
  name: "sluder",
  props: {
    listValue: Array,
  },
  data() {
    return {
      value: 0,
      maxRange: 500,
      max: 1000,
      start: [10],
      slider: {
        startMin: 25,
        startMax: 1000,
        start: 40,
        step: 10,
      },
      Slider: <HTMLElement>this.$refs.slider,
    };
  },
  watch: {},
  methods: {
    updateSlider(e: any) {
      (<any>this.$refs.slider).noUiSlider.set([this.value]);
    },
  },
  mounted() {
    this.Slider = <HTMLElement>this.$refs.slider;
    let last = this.listValue[this.listValue.length - 1];
    let rang =<any> {
      min: 25,
    };
    let point = "";
    this.listValue.reduce((sum: Number, current, i) => {
      point =
        ((100 / (this.listValue.length - 1)) * <number>sum).toFixed(0) + "%";
      rang[point] = [this.listValue[+sum], this.listValue[i]];
      return i;
    }, 0);
    rang["100%"] = [last, last];
    rang["max"] = last;

    noUiSlider.create(this.Slider, {
      start: <number>this.listValue[0],
      step: this.slider.step,
      connect: true,
      range: <any>rang,
      pips: {
        mode: "values",
        values: <number[]>this.listValue,
        density: 500,
      },
    });
    (<any>this.$refs.slider).noUiSlider.on("update", (value: number) => {
      this.value = value;
    });
  },
});
</script>
<style scoped lang="scss">
#slider-input {
  margin-top: 100px;
}
.slider{
  margin:50px;
}
</style>
