<template>
  <div id="app">
    <div class="calculator">
      <h1>Vue Calculator</h1>
      <div class="display">{{ display }}</div>
      <div class="buttons">
        <button @click="appendToDisplay('1')">1</button>
        <button @click="appendToDisplay('2')">2</button>
        <button @click="appendToDisplay('3')">3</button>
        <button @click="appendToDisplay('+')">+</button>
        <button @click="appendToDisplay('4')">4</button>
        <button @click="appendToDisplay('5')">5</button>
        <button @click="appendToDisplay('6')">6</button>
        <button @click="appendToDisplay('-')">-</button>
        <button @click="appendToDisplay('7')">7</button>
        <button @click="appendToDisplay('8')">8</button>
        <button @click="appendToDisplay('9')">9</button>
        <button @click="calculateResult()">=</button>
        <button @click="appendToDisplay('0')">0</button>
        <button @click="appendToDisplay('*')">*</button>
        <button @click="appendToDisplay('/')">/</button>
        <button @click="clearDisplay()">C</button>
      </div>
    </div>
    <div class="line"></div>
    <div class="history">
      <h2>Calculation History</h2>
      <button @click="clearHistory" class="clear-button">Clear</button>
      <ul class="history-list">
        <li v-for="(calculation, index) in history" :key="index">{{ calculation }}</li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      display: '',
      history: [],
      isError: false,
    };
  },
  methods: {
    appendToDisplay(value) {
      if (this.display.length > 23) {
        this.display = 'Zbyt długie';
        this.isError = true;
      } else if (this.isError) {
        this.display = value;
        this.isError = false;
      } else {
        this.display += value;
      }
    },
    calculateResult() {
      try {
        const result = eval(this.display).toString();
        this.history.unshift(`${this.display} = ${result}`);
        this.display = ''; 
      } catch (error) {
        this.display = 'Błąd';
        this.isError = true;
      }
    },
    clearDisplay() {
      this.display = '';
      this.isError = false;
    },
    clearHistory() {
      this.history = [];
    },
  },
};
</script>

<style>
body {
  background-color: #1d3557;
  color: black;
  margin: 0;
}

#app {
  text-align: center;
  margin-top: 60px;
}

.calculator {
  width: 300px;
  margin: 0 auto;
  border: 1px solid #ccc;
  padding: 10px;
  border-radius: 5px;
  background-color: #f1faee;
}

.display {
  font-size: 1.5em;
  margin-bottom: 10px;
  background-color: #457b9d;
  color: white;
  padding: 10px;
  border-radius: 5px;
  height: 20px;
}

.buttons {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-gap: 5px;
}

button {
  font-size: 1.2em;
  padding: 10px;
  cursor: pointer;
  background-color: #a8dadc;
  color: #1d3557;
  border: 1px solid #457b9d;
  border-radius: 5px;
}

.clear-button {
  font-size: 1em;
  padding: 5px;
  cursor: pointer;
  background-color: #e63946;
  color: white;
  border: 1px solid #b81c25;
  border-radius: 3px;
}

.history {
  margin-top: 20px;
  background-color: #1d3557;
  color: white;
}

.history h2 {
  font-size: 1.2em;
  margin-bottom: 5px;
}

.history-list {
  list-style: none;
  padding: 0;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-gap: 5px;
}

.history li {
  margin-bottom: 5px;
  color: white;
  box-sizing: border-box;
}

.line {
  height: 2px;
  width: 95%;
  background-color: white;
  margin: 10px auto;
}
</style>
