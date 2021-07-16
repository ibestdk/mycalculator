<template>
  <div class="calculator">
    <div class="display">{{showondisplay || '0'}}</div>
    <button @click="clear" class="btn c">C</button>
    <button @click="ercent" class="btn operator">%</button>
    <button @click="plus" class="btn operator">+</button>
    <button @click="minus" class="btn operator">-</button>
    <button @click="append('7')" class="btn">7</button>
    <button @click="append('8')" class="btn">8</button>
    <button @click="append('9')" class="btn">9</button>
    <button @click="multiply" class="btn operator">✕</button>
    <button @click="append('4')" class="btn">4</button>
    <button @click="append('5')" class="btn">5</button>
    <button @click="append('6')" class="btn">6</button>
    <button @click="divide" class="btn operator">÷</button>
    <button @click="append('1')" class="btn">1</button>
    <button @click="append('2')" class="btn">2</button>
    <button @click="append('3')" class="btn">3</button>
    <button @click="exponent" class="btn operator">^</button>
    <button @click="append('0')" class="btn zero">0</button>
    <button @click="dot" class="btn">.</button>
    <button @click="total" class="btn operator">=</button>

  </div>
</template>

<script>
export default {
  data(){
    return{
      showondisplay: '',
      previous: null,
      operator: null,
      operatorClicked: false,
    }
  },
  methods:{
    clear(){
      this.showondisplay = '' ;
    },
    append(nummber){
      if (this.operatorClicked){
        this.showondisplay = '';
        this.operatorClicked = false;
      }
      this.showondisplay = `${this.showondisplay}${nummber}`
    },
    dot(){
      if(this.showondisplay.indexOf('.') === -1){
        this.append('.');
      }
    },

    setPrenum(){
      this.previous = this.showondisplay;
      this.operatorClicked = true;
    },
    ercent(){
      this.showondisplay = `${parseFloat(this.showondisplay)/100}`
    },
    plus(){
      this.operator = (a,b) => a + b;
      this.setPrenum();
    },
    minus(){
      this.operator = (a,b) => b - a;
      this.setPrenum();
    },
    multiply(){
      this.operator = (a,b) => a * b;
      this.setPrenum();
    },
    divide(){
      this.operator = (a, b) => b / a;
      this.setPrenum();
    },
  
    exponent(){
      this.operator = (a,b) => Math.pow(b,a);
      this.setPrenum();
    },
    total(){
      this.showondisplay = `${this.operator(parseFloat(this.showondisplay), parseFloat(this.previous))}`;
      this.previous = null;
    },
  }
}
</script>





<style scoped>
.calculator {
  border-radius: 20px;
  background: gray;
  margin:0 auto;
  width: 400px;
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px , auto);
  
}

.display{
  margin: 20px;
  padding-right: 5%;
  padding-top: 5%;
  text-align:right;
  height: 70px;
  grid-column:  1/5;
  background-color: rgb(184, 184, 184);
  text-align: right center;
  color: white;
  font-weight: 600;
  border-radius: 10px;
}
.zero{
  grid-column: 1/3;
}


.btn{
  text-align: center;
  height: 80;
  background-color: rgb(240, 240, 240);
  border-radius: 20px;
  margin: 5px;
  font-weight: 600;
  font-size: 20px;
  
}

.operator{
background: rgb(63, 63, 63);
color: white;
}

.c{
  background: rgb(255, 194, 79);
  color: white;
}
</style>
