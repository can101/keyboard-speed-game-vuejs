<template>
  <div class="container">
    <div class="text-wrapper">
      <!-- <span>
        <span :class="[checkFunc('word'), 'text-word']">word</span>
      </span> -->

      <span
        v-for="item in text"
        :class="[checkFunc(item.value), 'text-word']"
        :key="item.id"
        :set-data="item.value"
        >{{ item.value }}</span
      >
    </div>
  </div>
</template>

<script>
export default {
  name:"GameText",
  emits: ["reset:word"],
  props: ["text", "worddata"],
  methods: {
    checkFunc(word) {
      if (this.worddata != "") {
        if (word == this.worddata) {
          // setTimeout(() => {
          this.$emit("reset:word");
          // }, 200);
          return "success";
        } else {
          return "text-danger";
        }
      }
    },
  },
};
</script>

<style scoped>
.container {
  padding: 5px 0;
}
.text-wrapper {
  display: flex;
  flex-wrap: wrap;
  color: #414042;
  letter-spacing: 1px;
  font-family: arial;
  max-width: 550px;
  width: 80%;
  margin: 0 auto;
  line-height: 1.5;
  user-select: none;
  cursor: none;
}
.text-word {
  margin-right: 5px;
}
.text-success {
  color: green;
}
.text-danger {
  color: red;
}
.success {
  animation: tracking-out-contract 0.5s linear both;
}
/* 0.7 */
.successAnim {
  position: relative;
}
.successAnim::after {
  content: "✓";
  position: absolute;
  background-color: #4bb543;
  box-shadow: inset 0 0 6px #fff;
  top: 0%;
  border-radius: 50%;
  width: 30px;
  height: 30px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 20px;
  color: #fff;
  animation: slide-and-blur-out 1.5s none;
  animation-delay: 0.9s;
}
@keyframes tracking-out-contract {
  0% {
    opacity: 1;
    color: #4bb543;
  }
  100% {
    letter-spacing: -0.5em;
    opacity: 0;
    visibility: hidden;
    display: none;
  }
}
@keyframes slide-and-blur-out {
  0% {
    opacity: 1;
  }
  100% {
    letter-spacing: -0.5em;
    opacity: 0;
    transform: translateY(-150%) rotate(360deg) scale(0.5);
    filter: blur(12px);
    display: none !important;
  }
}
</style>