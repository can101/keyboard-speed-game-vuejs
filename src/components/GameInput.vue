<template>
    <textarea
        placeholder="kelimeyi girip ardından enter tuşuna basınız"
        type="text"
        class="word_input"
        @input="handleChange"
        @keydown="handleKeyDown"
        @keypress.enter.prevent="checkValue"
        :value="worddata"
        autofocus="true"
    />
</template>

<script>
export default {
  emits: ["animate:keydowncharcter", "reset:word"],
  props: ["worddata"],
  methods: {
    handleChange(e) {
      this.$emit("change:inputvalue", e.target.value.trim());
    },
    handleKeyDown(e) {
      this.$emit("animate:keydowncharcter", e);
    },
    checkValue() {
      this.$emit("reset:word");
    },
  },
};
</script>

<style scoped>
.word_input {
  border: none;
  user-select: none;
  border: 2px solid #d3d6da;
  color: #414042;
  caret-color: #d3d6da;
  letter-spacing: 1px;
  padding: 10px;
  border-radius: 5px;
  display: block;
  margin: 10px auto;
  width: 510px;
  resize: none;
  height: 150px;
  outline: none;
  font-family: Arial;
  box-sizing: border-box;
}
@media (max-width: 990px) {
  .word_input {
    width: 95%;
  }

}
.word_input:focus {
  box-shadow: inset 0 0 2px #009aff, 0 0 8px #009aff;
  border-color: transparent;
}

</style>