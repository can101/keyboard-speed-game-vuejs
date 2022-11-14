<template>
  <div class="game-keyboard-wrapper">
    <kbd
        v-for="key in list"
        :set-data="key.code"
        :key="key.keyCode"
        :style="calculateColor(key.count)"
    >{{ key.key }}</kbd
    >
  </div>
</template>

<script>
export default {
  name: "heatSignatureMapListKeyboard",
  props: ["list"],
  methods: {
    calculateColor(count) {
      const c = count / 10+0.1;
      let bg = ""
      if (count == 0) {
        bg = 'background-color: #d3d6da;'
      } else if (count > 0 || 20 < count) {
        bg = `background-color: rgba(30,52,84,${c});color:#f5f5f5;`
      }
      if (count >= 20 || 50 < count) {
        bg = `background-color: rgba(86,141,115,${c});`
      }
      if (count >= 50 || 85 < count) {
        bg = `background-color: rgba(247,155,45,${c});`
      }
      if(count>=85){
        bg = `background-color: rgba(204,69,77,${c});color:#f5f5f5;`
      }
      return bg
    }
  }
}
</script>


<style scoped>
kbd {
  user-select: none;
  color: #414042;
  font-weight: 700;
  font-family: Arial;
  text-transform: uppercase;
  border-radius: 5px;
  width: 2.8rem;
  height: 3.5rem;
  display: flex;
  justify-content: center;
  align-items: center;
  border: none;
  background-color: #d3d6da;
  margin: 5px;
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
  max-height: 500px;
  max-width: 550px;
  width: 100%;
  margin: 0 auto;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

@media (max-width: 1200px) {
  kbd {
    width: 2.2rem;
    height: 3.3rem;
  }
}

@media (max-width: 1100px) {
  kbd {
    width: 2.25rem;
    height: 3.2rem;
  }
}

@media (max-width: 1000px) {
  kbd {
    width: 1.9rem;
    height: 3rem;
    font-size: 14px;
  }
}

@media (max-width: 900px) {
  kbd {
    width: 1.75rem;
    height: 2.9rem;
  }

  kbd[set-data="Space"] {
    width: 67%;
  }
}

@media (max-width: 830px) {
  kbd {
    width: 1.55rem;
    height: 2.9rem;
  }

  kbd[set-data="Space"] {
    width: 67%;
  }
}

@media (max-width: 760px) {
  kbd {
    width: 2.7rem;
    height: 2.9rem;
  }

  kbd[set-data="Space"] {
    width: 67%;
  }
}

@media (max-width: 560px) {
  kbd {
    width: 2.3rem;
    height: 2.9rem;
  }

  kbd[set-data="Space"] {
    width: 60%;
  }
}

@media (max-width: 430px) {
  kbd {
    width: 1.6rem;
    height: 2.9rem;
  }

  kbd[set-data="Space"] {
    width: 65%;
  }

  kbd[set-data="Backspace"] {
    width: 20%;
  }
}

@media (max-width: 395px) {
  kbd {
    width: 1.4rem;
    height: 2.9rem;
  }

  kbd[set-data="Space"] {
    width: 65%;
  }

  kbd[set-data="Backspace"] {
    width: 20%;
  }
}

@media (max-width: 365px) {
  kbd {
    width: 1.3rem;
    height: 2.9rem;
  }

  kbd[set-data="Space"] {
    width: 65%;
  }

  kbd[set-data="Backspace"] {
    width: 20%;
  }
}

@media (max-width: 280px) {
  kbd {
    width: 1.31rem;
    height: 2.9rem;
    font-size: 10px;
  }

  kbd[set-data="Space"] {
    width: 60%;
  }

  kbd[set-data="Backspace"] {
    width: 2.5rem;
  }

  kbd[set-data="Enter"] {
    width: 2.5rem;
  }
}
</style>