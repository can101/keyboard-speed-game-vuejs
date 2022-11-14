<template>
  <div class="container">
    <div class="game-keyboard-wrapper">
      <kbd
          v-for="key in props.list"
          :set-data="key.code"
          :class="[props.charcter.keyCode == key.keyCode ? 'active' : '']"
          :key="key.keyCode"
      >{{ key.key }}</kbd
      >
    </div>
  </div>
</template>

<script setup>
import {defineProps} from "vue";

const props = defineProps(["list", "charcter"]);
</script>

<style scoped>
kbd {
  user-select: none;
  color: #414042;
  font-weight: 700;
  font-family: Arial;
  text-transform: uppercase;
  border-radius: 5px;
  width: 40px;
  height: 58px;
  display: flex;
  justify-content: center;
  align-items: center;
  border: none;
  background-color: #d3d6da;
  margin: 5px;
}

.active {
  box-shadow: inset 0 0 2px #009aff, 0 0 8px #009aff;
  color: #49b3f7;
  text-shadow: 0 0 12px #009aff;
  background: #ffffff;
  transform: scale(1.5);
  z-index: 4;
}

@keyframes flipAnim {
  0% {
    transform: rotateX(0deg);
  }
  50% {
    transform: rotateX(90deg);
  }
  100% {
    transform: rotateX(0deg);
  }
}

@keyframes activeAnim {
  100% {
    box-shadow: inset 0 0 2px #009aff, 0 0 8px #009aff;
    color: #49b3f7;
    text-shadow: 0 0 12px #009aff;
    background: #ffffff;
    transform: scale(1.5);
  }
}

.anim {
  animation: 0.5s linear flipAnim;
}

kbd[set-data="Space"] {
  width: 70%;
  transform: scale(1);
}

kbd[set-data="Backspace"] {
  width: 65px;
  /* transform: scale(1); */
}

kbd[set-data="Enter"] {
  width: 60px;
  /* transform: scale(1); */
}

.game-keyboard-wrapper {
  /*background: red;*/
  max-height: 500px;
  width: 500px;
  margin: 0 auto;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.container {
  width: 100%;
  margin-top: 40px;
}

@media (max-width: 990px) {
  .container {
    display: none;
  }

}

</style>