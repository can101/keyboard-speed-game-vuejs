<template>
  <div :class="[data.count == 0 ? '' : 'overlay', 'counter_box']">
    <span>
      {{
        Math.floor(data.count / 60) < 10
          ? "0" + Math.floor(data.count / 60)
          : Math.floor(data.count / 60)
      }}
    </span>
    &#x2236;
    <span>
      {{
        Math.floor(data.count % 60) < 10
          ? "0" + Math.floor(data.count % 60)
          : Math.floor(data.count % 60)
      }}
    </span>
  </div>
</template>

<script setup>
import { reactive, defineEmits } from "vue";

const emit = defineEmits(["end:time"]);
let data = reactive({ count: 90 });

let loopTimer;

const decraseCounter = () => {
  data.count--;
  if (data.count < 1) {
    emit("end:time");
    clearInterval(loopTimer);
  }
};
loopTimer = setInterval(() => {
  decraseCounter();
}, 1000);
</script>

<style scoped>
.counter_box {
  user-select: none;
  color: #009aff;
  background: #cae7fa;
  box-shadow: inset 0 0 10px #ffffff;
  padding: 10px;
  border-radius: 5px;
  font-weight: 500;
  position: relative;
  overflow: hidden;
}
.overlay::after {
  position: absolute;
  content: "";
  width: 100%;
  height: 100%;
  top: 0;
  right: 0;
  display: block;
  background-color: #98cbed;
  animation: 1.19s both timerAnim infinite;
}
@keyframes timerAnim {
  from {
    transform: translateX(-100%);
    opacity: 1;
  }
  to {
    transform: translateX(0%) scale(2);
    opacity: 0;
  }
}
</style>