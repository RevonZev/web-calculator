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
        <!-- First - third column -->
        <button
          v-for="(text, index) in button_texts_a"
          :key="index"
          v-on:click.prevent="addCalculatorString($event)"
          v-bind:style="'grid-area:' + text[1]"
        >
          {{ text[0] }}
        </button>
      </div>
      <!-- Fourth column -->
      <div class="buttons-b">
        <button
          v-for="(text, index) in button_texts_b"
          :key="index"
          v-on:click.prevent="addCalculatorString($event)"
          v-bind:style="'grid-area:' + text[1]"
        >
          {{ text[0] }}
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
      // prettier-ignore
      button_texts_a: [
        ["1", "aa"], ["2", "ab"], ["3", "ac"],
        ["4", "ad"], ["5", "ae"], ["6", "af"],
        ["7", "ag"], ["8", "ah"], ["9", "ai"],
        ["0", "aj"], [".", "ak"], ["=", "al"],
      ],
      button_texts_b: [
        ["<", "ba"],
        ["/", "bb"],
        ["x", "bc"],
        ["+", "bd"],
        ["-", "be"],
      ],
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
      const exceptions = [".", "/", "+", "-"];
      var event_innerHTML = event.target.innerText;

      // Make the caret stay on the right end
      target.focus();
      target.setSelectionRange(-1, -1);
      target.blur();

      this.updateScreenLine(true);

      if (event_innerHTML.includes("<")) {
        // Backspace
        this.screen_text = this.screen_text.slice(0, -1);
        this.updateScreenLine();
        return 0;
      } else if (!isNaN(parseInt(event_innerHTML))) {
        // Numbers
        this.screen_text += event_innerHTML;
        return 0;
      } else if (event_innerHTML.includes("x")) {
        // Times
        this.screen_text += "*";
        return 0;
      } else if (event_innerHTML.includes("=")) {
        // Answer
        this.screen_text_question = this.screen_text;
        this.screen_text = eval(this.screen_text).toString();
        return 0;
      } else {
        // Decimal, devide, , add, subtract
        exceptions.forEach((exception) => {
          if (event_innerHTML.includes(exception)) {
            this.screen_text += event_innerHTML;
          }
        });
      }
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
  position: absolute;
  color: #131112;
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
  position: absolute;
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
  left: 23px;
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
  position: absolute;
  top: 0;
  left: 0;
  display: grid;
  /* prettier-ignore */
  grid-template: 
  "aa ab ac"
  "ad ae af"
  "ag ah ai"
  "aj ak al";
  grid-gap: 10px;
  width: 234px;
  height: 294px;
}

.buttons-b {
  position: absolute;
  top: 0;
  left: 234px;
  display: grid;
  /* prettier-ignore */
  grid-template: 
  "ba"
  "bb"
  "bc"
  "bd"
  "be";
  grid-gap: 10px;
  margin-left: 10px;
  width: 50px;
  height: 294px;
}

.buttons-a button {
  font-size: 55px;
  width: 100%;
  height: 100%;
  border-radius: 10px;
}

.buttons-b button {
  font-size: 30px;
  width: 100%;
  height: 100%;
  border-radius: 5px;
}

@media screen and (max-height: 475px) {
  .app-calculator {
    position: absolute;
    transform-origin: center;
    top: calc(50% - (340px / 2));
    left: calc(50% - (475px / 2));
    width: 475px;
    height: 340px;
    border-radius: 10px;
    background: #2e282a;
    box-shadow: -10px 10px 10px rgba(32, 36, 39, 0.63);
  }

  .calculator-screen {
    position: absolute;
    color: #131112;
    top: 20px;
    left: 20px;
    width: 430px;
    height: 72px;
    border-radius: 10px;
    background: #edddd4;
  }

  .screen-line {
    position: absolute;
    top: calc(50% - (58px / 2));
    left: 95%;
    width: 6px;
    height: 58px;
    border-radius: 10px;
    background: #289097;
    transform: scaleY(100%);
    transition: transform 300ms ease-in-out;
  }

  .screen-line-off {
    position: absolute;
    top: calc(50% - (58px / 2));
    left: 95%;
    width: 6px;
    height: 58px;
    border-radius: 10px;
    background: #289097;
    transform: scaleY(0%);
    transition: transform 300ms ease-in-out;
  }

  .screen-answer-text {
    position: absolute;
    top: calc(45% - (58px / 2));
    left: 1%;
    width: 395px;
    height: 58px;
    font-size: 64px;
    font-weight: 400;
    line-height: 77px;
    text-align: right;
    background: none;
    border: none;
  }

  .screen-question-text {
    display: none;
  }

  .calculator-buttons {
    display: flex;
    position: absolute;
    top: 110px;
    left: 13px;
    justify-content: space-around;
    flex-wrap: wrap;
  }

  .buttons-a {
    position: absolute;
    top: 0;
    left: 0;
    display: grid;
    /* prettier-ignore */
    grid-template: 
    "aa ab ac ad . ."
    "ae af ag ah . ."
    "ai aj ak al al al";
    grid-gap: 5px;
    width: 375px;
    height: 220px;
  }

  .buttons-b {
    position: absolute;
    top: 0;
    left: 305px;
    display: grid;
    /* prettier-ignore */
    grid-template: 
    "bd ba"
    "be bb"
    ". bc";
    grid-gap: 5px;
    margin-left: 10px;
    width: 135px;
    height: 220px;
  }

  .buttons-a button {
    font-size: 55px;
    width: 100%;
    height: 100%;
    border-radius: 10px;
  }

  .buttons-b button {
    font-size: 55px;
    width: 100%;
    height: 100%;
    border-radius: 5px;
  }
}
</style>
