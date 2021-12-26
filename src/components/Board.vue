<template>
  <div class="board">
    <Snake v-for="(elem, index) in snakeBody" :key="index" :snakeDot="elem" />
    <Food :foodCoord="foodCoord" />
  </div>
</template>

<script>
import Snake from "@/components/Snake";
import Food from "@/components/Food";
export default {
  name: "Board",
  components: {
    Snake,
    Food,
  },
  data() {
    return {
      snakeBody: [
        [0, 0],
        [2, 0],
      ],
      speed: 500,
      currentDirection: "ArrowRight",
      foodCoord: [],
    };
  },
  mounted() {
    document.body.addEventListener("keyup", (event) =>
      this.setDirection(event)
    );
    this.getRandCoord();
    setInterval(this.move, this.speed);
  },
  updated() {
    this.checkifOutOfBounds();
    this.checkIfCollapsed();
    this.checkIfEat();
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
    getRandCoord: function () {
      this.foodCoord = [];
      let num1 = Math.floor(Math.random() * 100);
      let num2 = Math.floor(Math.random() * 100);
      this.foodCoord.push(num1, num2);
    },
    setInitial: function () {
      this.snakeBody = [
        [0, 0],
        [2, 0],
      ];
      this.speed = 500;
      this.currentDirection = "ArrowRight";
    },
    checkifOutOfBounds: function () {
      let head = this.snakeBody[this.snakeBody.length - 1];

      if (head[0] >= 100 || head[1] >= 100 || head[0] < 0 || head[1] < 0) {
        this.onGameOver();
      }
    },
    checkIfCollapsed: function () {
      let dots = [...this.snakeBody];
      let head = dots[dots.length - 1];
      dots.pop();
      dots.forEach((dot) => {
        if (head[0] == dot[0] && head[1] == dot[1]) {
          this.onGameOver();
        }
      });
    },
    checkIfEat: function () {
      let dots = [...this.snakeBody];
      let head = dots[dots.length - 1];
        console.log(head[0],this.foodCoord[0], head[0] == this.foodCoord[0])
      if (head[0] == this.foodCoord[0] && head[1] == this.foodCoord[1]) {
        console.log("has eaten")
        this.getRandCoord();
        this.enlargeSnake();
        this.increaseSpeed();
      }
    },
    enlargeSnake: function () {
      let newSnake = [...this.snakeBody];
      newSnake.unshift([]);
      this.snakeBody = newSnake;
    },
    increaseSpeed: function () {
      if (this.speed > 10) {
        this.speed -= 10;
      }
    },
    onGameOver: function () {
      alert("Game Over. Snake length is " + this.snakeBody.length);
      this.setInitial();
    },
    move() {
      let dots = [...this.snakeBody];
      let head = dots[dots.length - 1];
      console.log(this.currentDirection);
      if (this.currentDirection == "ArrowRight") {
        head = [head[0] + 2, head[1]];
      } else if (this.currentDirection == "ArrowLeft") {
        head = [head[0] - 2, head[1]];
      } else if (this.currentDirection == "ArrowDown") {
        head = [head[0], head[1] + 2];
      } else if (this.currentDirection == "ArrowUp") {
        head = [head[0], head[1] - 2];
      }

      dots.push(head);
      dots.shift();
      this.snakeBody = [...dots];
    },
  },
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
