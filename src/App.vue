<template>
  <Main v-if="data.status" @change:status="chnageStatus"/>
  <div v-else>
    <a href="https://github.com/can101" target="_blank" class="github-link">Can Çelik</a>
    <div class="info-header">Oyunu başlatmak için enter butonuna tıklayınız</div>
    <div class="lottie-box">
      <lottie-animation
          class="lottieanim"
          :loop="true"
          :autoPlay="true"
          ref="anim"
          :animationData="require('@/assets/keyboard.json')"
      />
    </div>
    <div class="btn-wrapper">
      <svg
          @click.prevent="successStatus"
          width="36"
          height="44"
          viewBox="0 0 36 44"
          fill="none"
          class="enter-anim color_animation-enter"
          xmlns="http://www.w3.org/2000/svg"
      >
        <path
            d="M14.0909 23.9967L14.0909 22.9967L13.0909 22.9967L2.5 22.9967C2.29379 22.9967 1 22.5427 1 20.5L1 3.5C1 2.6439 1.20589 2.02418 1.51526 1.63563C1.79901 1.27926 2.24962 1.01426 3.00868 1L32 1C32.8514 1 33.5957 1.2148 34.1098 1.64322C34.5918 2.04491 35 2.74048 35 4L35 40C35 41.3028 34.6073 42.0099 34.1851 42.3999C33.7445 42.8068 33.1357 42.9939 32.5 42.9939L16.5 42.9939L16.4897 42.9939L16.4794 42.9941C15.5925 43.0124 15.0442 42.9879 14.6828 42.7787C14.4655 42.6529 14.0909 42.3212 14.0909 40.9943L14.0909 23.9967Z"
            fill="inherit"
            stroke="#1E3454"
            stroke-width="1.5"
        />
        <path
            fill-rule="evenodd"
            clip-rule="evenodd"
            d="M29.5 7.5V10.5C29.5 10.7761 29.2761 11 29 11H18V13.3868L13 10.5L18 7.61325V10H28.5V7.5H29.5Z"
            fill="#1E3454"
        />
      </svg>
    </div>
  </div>
</template>

<script setup>

import Main from "./components/Main.vue";
import {reactive, onMounted} from "vue";

let data = reactive({status: false});
const chnageStatus = () => {
  data.status = false;
};
const successStatus = () => {
  data.status = true;
};

const body = document.querySelector("body");
onMounted(() => {
  if (!data.status) {
    body.addEventListener("keypress", (event) => {
      if (event.code == "Enter") {
        successStatus();
      }
    });
  }
});
</script>

<style>
.lottieanim {
  width: 100%;
}

.btn-wrapper {
  position: absolute;
  bottom: 0;
  /*left: 10rem;*/
  height: 190px;
  width: 190px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.lottie-box {
  position: absolute;
  bottom: 0;
  right: 0;
  overflow: hidden;
  box-sizing: border-box;
}

.lottie-box svg {
  box-sizing: border-box;
  height: 700px !important;
}

body {
  background: #e7f6ff;
  box-sizing: border-box;
  padding: 0;
  margin: 0;
  overflow: hidden;
}

.enter-anim {
  transform: scale(3);
  fill: #2e5798;
  transition: all 1s;
  cursor: pointer;
  user-select: none;
}

.color_animation-enter {
  animation: colorAnim 1.5s linear alternate-reverse infinite;
}

.info-header {
  width: 100%;
  height: 70px;
  font-size: 1.3rem;
  letter-spacing: 1px;
  display: flex;
  align-items: center;
  justify-content: center;
  position: absolute;
  right: 0;
  font-family: Arial;
  z-index: 10;
}

.info-header::after {
  content: "\1F44B";
  font-size: 2rem;
  margin-left: 10px;
  transform-origin: 75% 75%;
  animation: wobble-horizontal-bottom 8s linear infinite;
}

@keyframes wobble-horizontal-bottom {
  0% {
    transform: rotate(0deg);
  }
  3% {
    transform: rotate(25deg);
  }
  6% {
    transform: rotate(-25deg);
  }
  9% {
    transform: rotate(0deg);
  }
}

@keyframes colorAnim {
  0% {
    transform: scale(4);
  }
  25% {
    fill: #f79b2d;
  }
  40% {
    transform: scale(3);
  }
  50% {
    fill: #cc454d;
  }
  60% {
    transform: scale(4);
  }
  75% {
    fill: #568d73;
  }
  80% {
    transform: scale(3);
  }
  100% {
    fill: #2e5798;
  }
}

@media (min-width: 990px) {
  .btn-wrapper {
    top: 10rem;
    left: 2rem;
  }

  .info-header {
    bottom: 0;
    left: 0;
  }
}

@media (max-width: 990px) {
  .btn-wrapper {
    bottom: 0;
    left: 0;
  }

  .info-header {
    top: 0;
    left: 0;
  }
}

@media (max-width: 768px) {
  .info-header {
    top: 0;
    font-size: .7rem;
  }

  .lottie-box svg {
    box-sizing: border-box;
    height: 600px !important;
  }

  .info-header::after {
    font-size: 1.3rem;
    margin-left: 3px;
  }
}

@media (max-width: 280px) {
  .info-header {
    font-size: .5rem;
  }

  .info-header::after {
    font-size: 1.3rem;
    margin-left: 5px;
  }
}

.github-link {
  text-decoration: none;
  font-family: Arial;
  border: 2px solid #ffcacd;
  color: #cc454d;
  letter-spacing: 1px;
  background-color: #ffcacd;
  padding: 7px 30px;
  border-radius: 108px;
  position: absolute;
  transform-origin: center;
  transform: rotate(270deg);
  right: -20px;
  bottom: 80px;
  cursor: pointer;
  box-sizing: border-box;
  z-index: 20;
  box-shadow: inset 0 0 10px #fff;
  transition: filter 1s ease-in-out;
}

.github-link:hover {
  filter: grayscale(10);
}


.github-link:hover {

}
</style>