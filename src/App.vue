<template>
  <div class="outputCalc">{{ calculatorValue || 0 }}</div>
  <div class="buttons">
    <div
      class="button"
      v-for="n in btnArr"
      :key="n"
      :class="{ operator: ['C', '*', '/', '-', '+', '%', '='].includes(n) }"
    >
      <div class="btn" @click="action(n)">
        {{ n }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      calculatorValue: "",
      btnArr: [
        "C",
        "*",
        "/",
        "-",
        "7",
        "8",
        "9",
        "+",
        "4",
        "5",
        "6",
        "%",
        "1",
        "2",
        "3",
        "=",
        "0",
        ".",
      ],
      operator: null,
      previousCalculatorValue: "",
    };
  },
  methods: {
    action(n) {
      /* Append value */
      if (!isNaN(n) || n === ".") {
        this.calculatorValue += n + "";
      }
      /* Clear value */
      if (n === "C") {
        this.calculatorValue = "";
      }
      /* Percentage */
      if (n === "%") {
        this.calculatorValue = this.calculatorValue / 100 + "";
      }
      /* Operators */
      if (["/", "*", "-", "+"].includes(n)) {
        this.operator = n;
        this.previousCalculatorValue = this.calculatorValue;
        this.calculatorValue = "";
      }
      /* Calculate result using the eval function */
      if (n === "=") {
        this.calculatorValue = eval(
          this.previousCalculatorValue + this.operator + this.calculatorValue
        );
        this.previousCalculatorValue = "";
        this.operator = null;
      }
    },
  },
};
</script>

<style>
.outputCalc {
  background-color: white;
  padding: 15px;
  border: 0.5px solid black;
  width: 20%;
  text-align: right;
  margin: auto;
  border-radius: 3px;
}

.buttons {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  width: min(300px, 70%);
  border: 0.2px solid black;
  border-radius: 4px;
  align-items: center;
  background-color: grey;
  justify-content: center;
  margin: 10px auto;
  gap: 5px;
}

.button {
  background-color: white;
  padding: 6px;
  border-radius: 3px;
  margin: 4px;
  font-size: 1.5em;
  font-weight: bold;
  color: #000;
  text-align: center;
  cursor: pointer;
  transition: all 0.2s ease-in-out;
}

.operator {
  background-color: lightgrey;
  color: #000;
}
</style>