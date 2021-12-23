<template>
  <div id="snake">
    <div
      class="body"
      v-for="(elem, index) in body"
      :key="index"
      :style="{ top: elem[0] + 'px', left: elem[1] + 'px' }"
    ></div>
  </div>
</template>
<script>
export default {
  name: "Snake",
  data() {
    return {
      body: [
        [0, 0],
        [0, 10],
      ],
      currentDirection: "ArrowRight",
    };
  },
  mounted() {
    document.body.addEventListener("keyup", (event) =>
      this.setDirection(event)
    );
    setInterval(this.move, 500);
  },

  methods: {
    setDirection: function (event) {
      if (
        event.key == "ArrowRight" ||
        event.key == "ArrowLeft" ||
        event.key == "ArrowDown" ||
        event.key == "ArrowUp"
      ) {
        this.currentDirection = event.key;
      }
    },
    move() {
      console.log(this.body[0]);
      this.body.forEach((elem) => {
        if (this.currentDirection == "ArrowRight") {
          let tempY = elem[0];
          let tempX = elem[1] + 10;

          this.body.shift();
          this.body.push([tempY, tempX]);
        } else if (this.currentDirection == "ArrowLeft") {
          let tempY = elem[0];
          let tempX = elem[1] - 10;

          this.body.shift();
          this.body.push([tempY, tempX]);
        } else if (this.currentDirection == "ArrowUp") {
          let tempY = elem[0] - 10;
          let tempX = elem[1];

          this.body.shift();
          this.body.push([tempY, tempX]);
        } else if (this.currentDirection == "ArrowDown") {
          let tempY = elem[0] + 10;
          let tempX = elem[1];

          this.body.shift();
          this.body.push([tempY, tempX]);
        }
      });
    },
  },
  computed: {},
};
</script>
<style scoped>
#snake {
  position: absolute;
  background-color: red;
}
.body {
  position: absolute;
  height: 10px;
  width: 11px;
  border: 2px solid white;
  z-index: 3;
  background-color: red;
}
</style>