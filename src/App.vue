<template>
  <div id="app">
    <slider :listValue="listValue" />
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import slider from './components/Slider.vue';

export default Vue.extend({
  name: 'App',
  data() {
    return {
      listValue:[25,30,35,40,45,50,75,100,150,200,300,400,500,750,1000]
    }
  },
  components: {
    slider
  }
});
</script>

<style lang="scss">

</style>
