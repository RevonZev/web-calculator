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
      <div class="screen-question-text">{{ screen_text_question }}</div>
    </div>
    <div class="calculator-buttons">
      <div class="buttons-a">
        <button
          v-for="(text, index) in button_texts_a"
          :key="index"
          v-on:click.prevent="addCalculatorString($event)"
        >
          {{ text }}
        </button>
      </div>
      <div class="buttons-b">
        <button
          v-for="(text, index) in button_texts_b"
          :key="index"
          v-on:click.prevent="addCalculatorString($event)"
        >
          {{ text }}
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      screen_has_text: false,
      screen_text: "",
      screen_text_question: "",
      button_texts_a: [
        "1", "2", "3",
        "4", "5", "6",
        "7", "8", "9",
        "0", ".", "=",
      ],
      button_texts_b: ["<", "/", "x", "+", "-"],
    };
  },
  methods: {
    updateScreenLine(force = false) {
      if (!force) {
        this.screen_has_text = this.screen_text != "" && !force ? true : false;
      } else {
        this.screen_has_text = true;
      }
    },
    addCalculatorString(event) {
      const target = document.getElementsByClassName("screen-answer-text")[0];
      const exceptions = [".", "/", "x", "+", "-"];
      var event_innerHTML = event.target.innerText;

      target.focus();
      target.setSelectionRange(0, 0)


      if (event_innerHTML.includes("<")) {
        this.screen_text = this.screen_text.slice(0, -1);
        this.updateScreenLine();
        return 0;
      } 
      
      this.updateScreenLine(true);

      if (!isNaN(parseInt(event_innerHTML))) {
        this.screen_text += event_innerHTML;
        return 0;
      }

      if (event_innerHTML.includes("x")) {
        this.screen_text += "*";
        return 0;
      } else if (event_innerHTML.includes("=")) {
        this.screen_text_question = this.screen_text;
        this.screen_text = eval(this.screen_text).toString();
        return 0;
      }

      exceptions.forEach(exception => {
        if (event_innerHTML.includes(exception)) {
          this.screen_text += event_innerHTML;
        }
      });
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

.calculator-buttons {
  display: flex;
  position: absolute;
  top: 160px;
  left: 20px;
  justify-content: space-around;
  flex-wrap: wrap;
}

.calculator-buttons button {
  background: #edddd4;
  color: #2c282a;
  border: 0;
  box-shadow: none;
}

.buttons-a {
  display: flex;
  flex-wrap: wrap;
  width: 234px;
  justify-content: space-between;
}

.buttons-b {
  display: flex;
  flex-wrap: wrap;
  width: 67px;
  justify-content: space-between;
  margin-left: 10px;
}

.buttons-a button {
  font-size: 55px;
  width: 67px;
  height: 67px;
  border-radius: 10px;
  margin-bottom: 10px;
}

.buttons-b button {
  font-size: 30px;
  width: 50px;
  height: 50px;
  border-radius: 5px;
  margin-bottom: 3px;
}
</style>
