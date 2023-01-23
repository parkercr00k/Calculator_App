<template>
  <div class="calculator">
    <div class="display">{{ current || "0" }}</div>
    <div v-on:click="clear" class="btn">C</div>
    <div v-on:click="sign" class="btn">+/-</div>
    <div v-on:click="percent" class="btn">%</div>
    <div v-on:click="divide" class="btn operator">/</div>
    <div v-on:click="append('7')" class="btn">7</div>
    <div v-on:click="append('8')" class="btn">8</div>
    <div v-on:click="append('9')" class="btn">9</div>
    <div v-on:click="times" class="btn operator">x</div>
    <div v-on:click="append('4')" class="btn">4</div>
    <div v-on:click="append('5')" class="btn">5</div>
    <div v-on:click="append('6')" class="btn">6</div>
    <div v-on:click="minus" class="btn operator">-</div>
    <div v-on:click="append('1')" class="btn">1</div>
    <div v-on:click="append('2')" class="btn">2</div>
    <div v-on:click="append('3')" class="btn">3</div>
    <div v-on:click="plus" class="btn operator">+</div>
    <div v-on:click="append('0')" class="btn" id="zero">0</div>
    <div v-on:click="dot" class="btn">.</div>
    <div v-on:click="equal" class="btn operator">=</div>
  </div>
</template>

<script>
export default {
  name: "CalculatorVue",
  data() {
    return {
      current: "",
      previous: null,
      operator: null,
      operatorClicked: false,
    };
  },

  methods: {
    clear() {
      this.current = "";
    },

    sign() {
      if (this.current == "" || this.current == "0") {
        this.current = "";
      } else if (this.current.includes("-", 0)) {
        this.current = this.current.slice(1);
      } else {
        this.current = "-" + this.current;
      }
    },

    percent() {
      this.current = `${parseFloat(this.current) / 100}`;
    },

    dot() {
      if (this.current.includes(".")) {
        this.current += "";
      } else {
        this.current += ".";
      }
    },

    append(number) {
      if (this.current === "" || this.current === "0") {
        this.current = number;
      } else {
        if (this.operatorClicked) {
          this.current = "";
          this.operatorClicked = false;
        }

        this.current = `${this.current}${number}`;
      }
    },

    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },

    plus() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },

    minus() {
      this.operator = (a, b) => b - a;
      this.setPrevious();
    },

    times() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },

    divide() {
      this.operator = (a, b) => b / a;
      this.setPrevious();
    },

    equal() {
      this.current = `${this.operator(
        parseFloat(this.current),
        parseFloat(this.previous)
      )}`;

      if(this.current == 'NaN' || this.current == 'undefined' || this.current == 'Infinity'){
        this.current = 'Error';
      }

      this.previous = null;
    },
  },
};
</script>

<style scoped>
.calculator {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  width: 400px;
  margin: 0 auto;
  box-shadow: 5px 5px 5px #333;
  margin-top: 150px;
}

.display {
  display: flex;
  align-items: center;
  justify-content: center;
  grid-column: 1 / 5;
  background-color: #333;
  color: white;
  font-size: 2rem;
}

#zero {
  grid-column: 1 / 3;
}

.btn {
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 2em;
  background-color: #eee;
  border: 1px solid #999;
}

.operator {
  background-color: orange;
  color: white;
}
</style>
