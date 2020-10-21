<template>
 <div class="container">
  <div class="calculator">
      <p class="btn display">{{current || 0}}</p>
      <div @click="clear" class="btn">C</div>
      <div @click="sign" class="btn operator">+/-</div>
      <div @click="persent" class="btn operator">%</div>
      <div @click="divide" class="btn operator">/</div>
      <div @click="append(7)" class="btn">7</div>
      <div @click="append(8)" class="btn">8</div>
      <div @click="append(9)" class="btn">9</div>
      <div @click="multiply" class="operator btn">x</div>
      <div @click="append(4)" class="btn">4</div>
      <div @click="append(5)" class="btn">5</div>
      <div @click="append(6)" class="btn">6</div>
      <div @click="minus" class="btn operator">-</div>
      <div @click="append(1)" class="btn">1</div>
      <div @click="append(2)" class="btn">2</div>
      <div @click="append(3)" class="btn">3</div>
      <div @click="append(0)" class="btn">0</div>
      <div @click="add" class="btn operator">+</div>
      <div @click="dot" class="btn operator">.</div>
      <div @click="equal" class="btn eq">=</div>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return{
      current: '',
      operator: null,
      previous:null,
      operatorClicked:false

    }
  },
  methods:{
    clear(){
      this.current = '';
    },
    sign(){
      this.current = this.current.charAt(0) === '-'?
        this.current.slice(1): '-' + this.current;
    },
    persent(){
      this.current = String(parseInt(this.current)/100)
    },
    append(number){
      if (this.operatorClicked){
        this.current='';
        this.operatorClicked = false;
      }
      this.current = this.current + number; 
    },
    dot(){
      this.current = this.current + "."; 
    },
    divide(){
      this.operator = (a,b) => a / b;
      this.setPrev();
    },
     add(){
      this.operator = (a,b) => a + b;
      this.setPrev();
    },
     minus(){
      this.operator = (a,b) => a - b;
      this.setPrev();
    },
     multiply(){
      this.operator = (a,b) => a * b;
      this.setPrev();
    },
    equal(){

      this.current = this.operator(parseFloat(this.current),parseFloat(this.previous));
      this.previous = null;


    },
    setPrev(){
      this.previous = this.current;
      this.operatorClicked= true;

    }

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container{
  width: 50%;
  align-content: center;
  padding-left: 20%;
}
.calculator{
  display: grid;
  grid-template-columns: repeat(4,1fr);
  grid-auto-rows: minmax(50px, auto) ;
}

.display{
  grid-column: 1/5;
  background-color: azure;
}
.eq{
  grid-column: 1/3;
}
.operator{
  background-color: darkorange; 
}
.btn{
  border: 1px solid #333;
  
}
</style>
