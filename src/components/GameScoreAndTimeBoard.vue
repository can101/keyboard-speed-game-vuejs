<template>
  <div class="container">
    <span class="container-inner">
      <GameCounterVue @end:time="endGame" :status="status" />
    </span>
  </div>
</template>

<script>
import GameCounterVue from "./GameCounter.vue";
export default {
  name: "GameScoreAndTimeBoard",
  props:["status"],
  emits: ["end:game", "start:game"],
  components: {
    GameCounterVue,
  },
  methods: {
    endGame() {
      this.$emit("end:game");
    },
    startGame() {
      this.$emit("start:game");
    },
  },
};
</script>

<style scoped>
.container {
  position: absolute !important;
  top: 0;
  display: flex;
  width: 100%;
  justify-content: center;
  font-family: Arial;
}
.container-inner {
  /* background: red; */
  height: 50px;
  max-width: 100%;
  gap: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>