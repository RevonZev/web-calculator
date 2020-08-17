<template>
  <div class="app-calculator">
    <div class="calculator-screen">
      <div
        v-bind:class="{
          'screen-line': screen_has_text,
          'screen-line-off': !screen_has_text,
        }"
      ></div>
      <input
        type="text"
        class="screen-answer-text"
        v-on:input="updateScreenLine()"
        v-model="screen_text"
      />
      <div class="screen-question-text">{{ screen_text_answer }}</div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      screen_has_text: false,
      screen_text: "",
      screen_text_answer: "",
    };
  },
  methods: {
    updateScreenLine() {
      this.screen_has_text = this.screen_text != "" ? true : false;
    },
  },
};
</script>

<style scoped>
.app-calculator {
  position: absolute;
  transform-origin: center;
  top: calc(50% - (475px / 2));
  left: calc(50% - (340px / 2));
  width: 340px;
  height: 475px;
  border-radius: 10px;
  background: #2e282a;
  box-shadow: -10px 10px 10px rgba(32, 36, 39, 0.63);
}

.calculator-screen {
  color: #131112;
  position: relative;
  top: 20px;
  left: 20px;
  width: 301px;
  height: 124px;
  border-radius: 10px;
  background: #edddd4;
}

.screen-line {
  position: absolute;
  top: calc(50% - (103px / 2));
  left: 95%;
  width: 6px;
  height: 103px;
  border-radius: 10px;
  background: #289097;
  transform: scaleY(100%);
  transition: transform 300ms ease-in-out;
}

.screen-line-off {
  position: absolute;
  top: calc(50% - (103px / 2));
  left: 95%;
  width: 6px;
  height: 103px;
  border-radius: 10px;
  background: #289097;
  transform: scaleY(0%);
  transition: transform 300ms ease-in-out;
}

.screen-answer-text {
  position: absolute;
  top: calc(40% - (94px / 2));
  left: 5%;
  width: 261px;
  height: 80px;
  font-size: 64px;
  font-weight: 400;
  line-height: 77px;
  text-align: right;
  background: none;
  border: none;
  caret-color: rgba(0, 0, 0, 0);
}

.screen-question-text {
  position: relative;
  top: calc(75% - (30px / 2));
  left: 5%;
  width: 261px;
  height: 30px;
  font-size: 24px;
  font-weight: 400;
  line-height: 30px;
  text-align: right;
  background: none;
  border: none;
}
</style>
