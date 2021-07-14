<template>
  <div
    class="p-3"
    style="max-width: 400px; margin: 50px auto; background: #234"
  >
    <!--calculate result -->
    <div
      class="
        w-full
        rounded
        m-1
        p-3
        text-right
        lead
        font-weight-bold
        text-white
        bg-vue-dark
      "
    >
      {{ calculatorValue || 0 }}
    </div>

    <!-- CALCULATOR buttons -->
    <div class="row">
      <div class="col-3" v-for="n in calculatorElements" :key="n">
        <div
          class="lead text-white text-center m-1 py-3 bg-vue-dark h"
          @click="action(n)"
          :class="{
            'bg-vue-green': ['/', '+', '-', '*', 'c', '%', '='].includes(n),
          }"
        >
          {{ n }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Calculator",
  data() {
    return {
      calculatorValue: "",
      operator: null,
      previousCalculatorValue: "",
      calculatorElements: [
        "c",
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
        1,
        2,
        3,
        "=",
        "0",
        ".",
      ],
    };
  },
  methods: {
    action(n) {
      if (!isNaN(n) || n === ".") {
        this.calculatorValue += n;
      }
      if (n === "c") {
        this.calculatorValue = "";
      }
      if (n === "%") {
        this.calculatorValue = this.calculatorValue / 100;
      }
      if (["/", "+", "-", "*"].includes(n)) {
        this.operator = n;
        this.previousCalculatorValue = this.calculatorValue;
        this.calculatorValue = "";
      }
      if (n === "=") {
        this.calculatorValue = eval(
          this.previousCalculatorValue + this.operator + this.calculatorValue
        );

        this.operator = null;
        this.previousCalculatorValue = "";
      }
    },
  },
};
</script>

<style>
.bg-vue-dark {
  background: #31475e;
}
.h:hover {
  cursor: pointer;
  background: #3d5875;
}
.bg-vue-green {
  background: #3fb984;
}
</style>
