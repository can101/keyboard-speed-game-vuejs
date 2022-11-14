<template>
  <div class="container">
    <div class="correct-box">{{ netCorrectIncorrect?.correct }}</div>
    <div class="incorrect-box">{{ netCorrectIncorrect?.incorrect }}</div>
  </div>
</template>

<script>
export default {
  name: "NetScoreTable",
  props: ["netCorrectIncorrect"]
}
</script>

<style scoped>
.container {
  margin: 20px 0;
  display: flex;
  justify-content: center;
  user-select: none;
}

.correct-box, .incorrect-box {
  width: 100%;
  text-align: center;
  padding: 5px;
  color: #fff;
  font-weight: 600;
  letter-spacing: 1px;
}

.correct-box {
  color: #568D73;
}

.correct-box::before {
  content: "✓";
  margin-right: 10px;
}

.incorrect-box {
  color: #CC454D;
}

.incorrect-box::before {
  content: "✕";
  margin-right: 10px;
}
</style>