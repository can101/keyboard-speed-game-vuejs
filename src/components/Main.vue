<template>
  <GameModal v-if="mshow" @close:modal="closeModal" :heatSignatureMapList="heatSignatureMapList" :chart="chart"
             :heatSignatureKeyUnList="heatSignatureKeyUnList"/>
  <GameScoreAndTimeBoard @end:game="endGame" :status="status"/>
  <div class="container-box">
    <div class="box">
      <div>
        <GameInput
            @animate:keydowncharcter="kbdChracter"
            @change:inputvalue="changeInput"
            @reset:word="resetWord"
            :worddata="word"
        />
        <GameKeyboard :charcter="animCharcter" :list="list"/>
      </div>
      <div>
        <div class="container">
          <div class="text-wrapper">
            <span
                v-for="item in text"
                :class="[
                item.isStatus && 'success text-success successAnim',
                item.isStatus == false && 'success text-danger dangerAnim',
                'text-word',
              ]"
                v-show="item.isShow"
                :key="item.id"
                :set-data="item.value"
            >{{ item.value }}</span
            >
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import GameKeyboard from "./GameKeyboard.vue";
import GameInput from "./GameInput.vue";
import GameScoreAndTimeBoard from "./GameScoreAndTimeBoard.vue";
import randomSentence from "random-paragraph";
import GameModal from "@/components/Modal";

export default {
  name: "GameMain",
  emits: ["change:status"],
  components: {
    GameModal,
    GameScoreAndTimeBoard,
    GameKeyboard,
    GameInput,
    // GameText,
  },
  expose: ["word"],
  data() {
    return {
      list: [
        {key: "q", code: "KeyQ", keyCode: 81},
        {key: "w", code: "KeyW", keyCode: 87},
        {key: "e", code: "KeyE", keyCode: 69},
        {key: "r", code: "KeyR", keyCode: 82},
        {key: "t", code: "KeyT", keyCode: 84},
        {key: "y", code: "KeyY", keyCode: 89},
        {key: "u", code: "KeyU", keyCode: 85},
        {key: "i", code: "KeyI", keyCode: 73},
        {key: "o", code: "KeyO", keyCode: 79},
        {key: "p", code: "KeyP", keyCode: 80},
        {key: "a", code: "KeyA", keyCode: 65},
        {key: "s", code: "KeyS", keyCode: 83},
        {key: "d", code: "KeyD", keyCode: 68},
        {key: "f", code: "KeyF", keyCode: 70},
        {key: "g", code: "KeyG", keyCode: 71},
        {key: "h", code: "KeyH", keyCode: 72},
        {key: "j", code: "KeyJ", keyCode: 74},
        {key: "k", code: "KeyK", keyCode: 75},
        {key: "l", code: "KeyL", keyCode: 76},
        {key: "z", code: "KeyZ", keyCode: 90},
        {key: "x", code: "KeyX", keyCode: 88},
        {key: "c", code: "KeyC", keyCode: 67},
        {key: "v", code: "KeyV", keyCode: 86},
        {key: "b", code: "KeyB", keyCode: 66},
        {key: "n", code: "KeyN", keyCode: 78},
        {key: "m", code: "KeyM", keyCode: 77},
        {key: ",", code: "Comma", keyCode: 188},
        {key: ".", code: "Period", keyCode: 190},
        {key: "⌫", code: "Backspace", keyCode: 8},
        {key: "Space", code: "Space", keyCode: 32},
        {key: "⇧", code: "Shift", keyCode: 16},
        {key: "↵", code: "Enter", keyCode: 13},
      ],
      heatSignatureMapList: null,
      heatSignatureKeyUnList: 0,
      text: null,
      animCharcter: {},
      word: "",
      id: 0,
      status: false,
      mshow: false,
      chart: null,
    };
  },
  watch: {
    async id(newID) {
      if (newID == this.text.length - 20) {
        const newText = await this.genareteText(3, 3);
        this.text = await this.text.concat(newText);
      }
    },
  },
  methods: {
    closeModal() {
      this.mshow = false
      this.$emit("change:status");
    },
    openModal() {
      this.mshow = true
    },
    async genareteText(max = 7, min = 7) {
      return randomSentence({max, min})
          .split(" ")
          .map((value, index) => ({
            id: index,
            value,
            gusess: "",
            isStatus: null,
            isShow: true,
          }));
    },
    changeInput(e) {
      this.word = e;
    },
    async increasHeatSignatureMapKeyCount({keyCode}) {
      try {
        const index = await this.heatSignatureMapList.findIndex(
            (key) => key.keyCode == keyCode
        );
        this.heatSignatureMapList[index].count++;
      } catch (err) {
        this.heatSignatureKeyUnList++
      }
    },
    kbdChracter(e) {
      this.increasHeatSignatureMapKeyCount(e);
      this.animCharcter = e;
      setTimeout(() => {
        this.animCharcter = {};
      }, 250);
    },
    async resetWord() {
      if (this.word != "") {
        this.text[this.id].gusess = await this.word;
        this.text[this.id].isStatus = (await (this.word ==
            this.text[this.id].value))
            ? true
            : false;
        // this.text[this.id].isShow = await false;
        setTimeout(() => {
          this.text[this.id - 1].isShow = false;
        }, 110);
        this.id++;
        this.word = "";
      }
    },
    startGame() {
      this.status = true;
      console.log("game start");
    },
    async calculateChartData() {
      let i = 0,
          correct = 0,
          incorrect = 0,
          correctMatch = [];
      while (this.id - 1 >= i) {
        this.text[i].isStatus ? correct++ : incorrect++;
        await correctMatch.push(this.text[i]);
        i++;
      }
      let obj = await {
        correct,
        incorrect,
        correctMatch,
      };
      this.chart = obj
    },
    async endGame() {
      this.status = false;
      this.mshow = true;
      this.openModal()
      // this.$emit("change:status");
      await this.calculateChartData();
      console.log("game ended");
    },
  },
  async mounted() {
    this.text = await this.genareteText();
    this.heatSignatureMapList = await this.list.map((el) => ({
      ...el,
      count: 0,
    }));
  },
};
</script>

<style scoped>
.center {
  height: 100vh;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.container-box {
  height: 100vh;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.box {
  width: 95%;
  margin: 0 auto;
  display: flex;
}

.box > div {
  width: 100%;
}

.box > div:first-child {
}

.box > div:last-child {
  display: flex;
}

@media (max-width: 990px) {
  .box {
    flex-direction: column-reverse;
  }

}


.main {
  width: 90%;
  height: 80vh;
  display: flex;
  align-items: center;
  justify-content: center;
}

.text-wrapper {
  display: flex;
  flex-wrap: wrap;
  color: #414042;
  letter-spacing: 1px;
  font-family: arial;
  /*width: 100%;*/
  margin: 0 auto;
  padding: 7px 30px 0;
  line-height: 1.5;
  user-select: none;
  cursor: none;
}

@media (max-width: 990px) {
  .text-wrapper {
    height: 200px;
    overflow: hidden;
    padding: 10px;
    /*background-color: #49b3f7;*/
    margin: 0 auto 30px;
  }

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
  animation: tracking-out-contract 0.2s linear both;
}

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
  animation: slide-and-blur-out 0.4s none;
}

.dangerAnim {
  position: relative;
}

.dangerAnim::after {
  content: "✕";
  position: absolute;
  background-color: red;
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
  animation: slide-and-blur-out 0.4s none;
}

@keyframes tracking-out-contract {
  0% {
    opacity: 1;
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

body {
  background-color: #fff !important;
  overflow: hidden !important;
}
</style>
