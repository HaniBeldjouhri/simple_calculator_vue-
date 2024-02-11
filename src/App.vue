<template>
  <div id="app">
    <div class="title span4">{{ displayText }}</div>
    <div class="grid">
      <button v-for="char in every" :key="char" @click="handleClick(char)" :class="{ 'span2': char === '=' || char === 'Ac' }">{{ char }}</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      displayText: '',
      lastCharIsOperator: false,
      operators: ['+', '-', '*', '/', '.'],
      every: ['Ac', 'Del', '/', '1', '2', '3', '*', '4', '5', '6', '+', '7', '8', '9', '-', '.', '0', '=']
    };
  },
  methods: {
    handleClick(char) {
      if (char === '=') {
        this.calculate();
      } else if (char === 'Ac') {
        this.clearDisplay();
      } else if (char === 'Del') {
        this.deleteLastChar();
      } else {
        this.appendText(char);
      }
    },
    appendText(char) {
      this.displayText += char;
      this.lastCharIsOperator = this.operators.includes(char);
    },
    clearDisplay() {
      this.displayText = '';
      this.lastCharIsOperator = false;
    },
    deleteLastChar() {
  let textArr = this.displayText.toString().split('');
  textArr.pop();
  this.displayText = textArr.join('');
  this.lastCharIsOperator = this.operators.includes(textArr[textArr.length - 1]);
},
    calculate() {
      if (!!this.displayText) {
        this.displayText = eval(this.displayText);
      }
    }
  }
};
</script>

<style>
       .title{
            height: 100px;
            padding: 5px;
            border-radius:5px ;
            margin: 5px;
            color: white;
            background-color: rgb(43, 42, 42);
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            overflow: hidden;
            font-size: xx-large;
        }
        .grid{
            display: grid;
            grid-template-columns: auto auto auto auto;
        }
        button{
            padding: 30px;
            margin: 5px;
            border: 0;
            color: white;
            background-color: grey;
            border-radius:5px ;
            font-size: 20px;
            cursor: pointer;
        }
        .span2{
            grid-column: span 2;
        }
        .span4{
            grid-column: span 4;
        }
        button:hover{
            background-color: darkgrey;
        }
</style>
