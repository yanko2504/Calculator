<template>
<div class="calculator">
  <div class="display">{{current || '0'}}</div>
  <div @click="clear" class="button, c">C</div>
  <div @click="sign" class="button, special">+/-</div>
  <div @click="percent" class="button, special">%</div>
  <div @click="divide" class="button, special">÷</div>
  <div @click="append ('7')" class="button, ">7</div>
  <div @click="append ('8')" class="button">8</div>
  <div @click="append ('9')" class="button">9</div>
  <div @click="times" class="button, special">×</div>
  <div @click="append ('4')" class="button">4</div>
  <div @click="append ('5')" class="button">5</div>
  <div @click="append ('6')" class="button">6</div>
  <div @click="minus" class="button, special">-</div>
  <div @click="append ('1')" class="button">1</div>
  <div @click="append ('2')" class="button">2</div>
  <div @click="append ('3')" class="button">3</div>
  <div @click="add" class="button, special">+</div>
  <div @click="append ('0')" class="button">0</div>
  <div @click="append (',')" class="button, special">,</div>
  <div @click="equal" class="button, equals">=</div>
</div>
</template>

<script>
export default {
  data () {
    return {
      previous: null,
      current: '123',
      operator: null,
      operatorClicked: false,
    }
  },
  methods: {
    clear() {
      this.current = '';
    },
    sign() {
      this.current = this.current.charAt(0) === '-' ?
      this.current.slice(1) : `-${this.current}`;
    },
    percent() {
      this.current = `${parseFloat(this.current)/ 100}`
    },
    append(number){
      if(this.operatorClicked){
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },
    dot(){
      if(this.current.indexOf(',') === -1) {
        this.append(',');
      }
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked =  true;
    },
    divide(){
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    times(){
      this.operator = (a, b) => a * b;
      this.setPrevious();

    },
    minus(){
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    add(){
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    equal(){
      this.current = `${this.operator(
          parseFloat(this.current),
          parseFloat(this.previous)
      )}`;
      this.previous = nulll;
    }
  }
}
</script>

<style scoped>
.calculator {
  margin: 0 auto;
  width: 400px;
  front-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}
.display{
  grid-column: 1 / 5;
  background: #333;
  color: white;
}
.button{
  background-color: #008080;
  border: 1px solid #999;
  color: white;

}
.c{
  color: coral;
}
.special {
  color: green;
}
.equals{
  color: white;
  background-color: green;

}
</style>