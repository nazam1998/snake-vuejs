<template>
  <div
    class="food"
    :style="{ top: coord[0] + 'px', left: coord[1] + 'px' }"
  ></div>
</template>
<script>
export default {
  name: "Food",
  data() {
    return {
      coord: [],
    };
  },
  mounted() {
    this.getRandCoord();
  },
  methods: {
    getRandCoord() {
      this.coord = [];
      let num1 = Math.floor(Math.random() * 560);
      let num2 = Math.floor(Math.random() * 560);
      this.coord.push(num1, num2);
      console.log(this.coord);
    },
  },
};
</script>
<style scoped>
.food {
  position: absolute;
  height: 10px;
  width: 11px;
  border: 2px solid white;
  z-index: 3;
  background-color: green;
}
</style>