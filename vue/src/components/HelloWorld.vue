<template>
  <div class="hello">
    <h1>{{ message }}</h1>
    <!--
    <input type="text" :value="message @input="changeInput"/>
   <button @click="someMethodClick" v-bind:disabled="disabled"></button>
   -->
    <input type="text" v-model.number="operand1" />
    <input type="text" v-model.number="operand1" />

    = {{ result }}
    <br />
    <div class="strange-message">
      <template v-if="result < 0 ">Получилось отрицательное число</template>
      <template v-else-if="result < 110 ">Результат в первой сотне</template>
      <template v-else>Слишком большое число</template>
    </div>
  
    <hr />
    <button @click="calculate('+')">+</button>
    <button @click="calculate('-')">-</button>
    <button @click="calculate('/')">/</button>
    <button @click="calculate('*')">*</button>
    <hr/>
    {{ myCollection }}
    <div v-for="(item, index) in myCollection" :key="index">
      {{ index }} --{{ item }}
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data() {
    return {
      disabled: false,
      message: "",
      operand1: 0,
      operand2: 0,
      result: 0,
      error: "",
      myCollection: [1,2,3,4,5,6,7,9]
    };
  },
  methods: {
    calculate(operation = "+") {
      switch (operation) {
        case "+":
          this.add();
          break;
        case "-":
          this.substract();
          break;
        case "/":
          this.divide();
          break;
        case "*":
          this.multiply();
          break;
      }
    },
    add() {
      this.result = this.operand1 + this.operand2;
    },
    substract() {
      this.result = this.operand1 - this.operand2;
    },
    divide() {
      const { operand1, operand2 } = this;
      if (operand2 === 0) {
        this.error = "На ноль делить нельзя";
        return;
      }
      this.result = operand1 / operand2;
    },
    multiply() {
      this.result = this.operand1 * this.operand2;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
