<template>
    <div class="calculator">
      <div class="display">{{display}}</div>
      <div @click="clear" class="btn">AC</div>
      <div @click="sqrt" class="btn">√</div>
      <div @click="sign" class="btn">+/-</div>
      <div @click="divide" class="btn operator">÷</div>
      <div @click="append('7')" class="btn">7</div>
      <div @click="append('8')" class="btn">8</div>
      <div @click="append('9')" class="btn">9</div>
      <div @click="multi" class="btn operator">x</div>
      <div @click="append('4')" class="btn">4</div>
      <div @click="append('5')" class="btn">5</div>
      <div @click="append('6')" class="btn">6</div>
      <div @click="decrease" class="btn operator">-</div>
      <div @click="append('1')" class="btn">1</div>
      <div @click="append('2')" class="btn">2</div>
      <div @click="append('3')" class="btn">3</div>
      <div @click="add" class="btn operator">+</div>
      <div @click="zero" class="btn zero">0</div>
      <div @click="dot" class="btn">.</div>
      <div @click="equal" class="btn operator">=</div>
    </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      display: '',
      operator: null,
      operatorUsed: false,
    }
  },
  methods: {
    append(number) {
      if(this.operatorUsed) {
        this.display = ''
        this.operatorUsed = false
      }
      this.display = `${this.display}${number}`
    },
    clear() {
      this.display = ''
      this.previous = null
    },
    setPrevious() {
      this.previous = this.display
      this.operatorUsed = true;
    },
    equal() {
      if(this.previous !== null) {
      this.display = this.operator(parseFloat(this.previous), parseFloat(this.display))
      this.previous = null
      this.operatorUsed = true;
      }
    },
    add() {
      this.operator = (a,b) => a+b
      this.setPrevious()
    },
    decrease() {
      this.operator = (a,b) => a-b
      this.setPrevious()
    },
    divide() {
      this.operator = (a,b) => a/b
      this.setPrevious()
    },
    multi() {
      this.operator = (a,b) => a*b
      this.setPrevious()
    },
    sqrt() {
      this.display = Math.sqrt(this.display)
      this.setPrevious();
    },
    sign() {
      if(this.display[0] === '-') {
        this.display = this.display.slice(1)
      } else {
        this.display = `-${this.display}`
      }
    },
    dot() {
    //this function only appends '.' if it hasn't shown before
    //also can use this.display.includes('.')
      if(this.display.indexOf('.') === -1) {
        this.append('.')
      }
    },
    zero() {
      if(this.display.charAt(0) !== '0' || this.display.charAt(1) === '.') {
        this.append('0')
      }
    }
  }
}
</script>

<style scoped>
.calculator {
    margin: 0 auto;
    width: 300px;
    font-size: 30px;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: minmax(40px, auto);
    border: 2px solid black;
}
.display{
    grid-column: 1/5;
    color:blanchedalmond;
    background-color: black;
    text-align: center;
    padding: 2%;
}
.zero{
    grid-column: 1/3;
}
.btn{
    background-color: #eee;
    border: 2px solid black;
}
.operator{
    background-color: yellowgreen;
    color: whitesmoke;
}
</style>