<template>
  <div class="board">
    <Snake/>
    <Food/>
  </div>
</template>

<script>
import Snake from '@/components/Snake';
import Food from '@/components/Food';
export default {
  name: "Board",
  components: {
    Snake,
    Food,
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.board {
  position: relative;
  height: 600px;
  width: 600px;
  background: #000;
  margin: 20px auto;
}
</style>
