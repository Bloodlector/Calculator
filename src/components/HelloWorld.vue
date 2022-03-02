<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <hr/>    
    <div class="display">
      <span>  Число 1 = </span><input v-model="operand1" type="text">
      <span>  Число 2 = </span><input v-model="operand2" type="text"><br>
      <span>Результат  </span>= {{ result }}
    </div>    
    <div class="keyboard">
      <button v-for="(operand, idx) in operands"
      :key="operand"
      :name="operand"
      :id="idx +1"
      class='btns'
      :disabled='getBtnStatusDisabled(operand)'
      @click="calculate(operand)">
        {{operand}}
      </button>
    </div>
    <div class="displayButton">
      <input type="checkbox" id="checkbox" v-model="checkbox"><span> Экранная клавиатура</span>
        <div class="keyboard" v-if="checkbox">
          <div class="row">
                  <div class="keyboard">
        <button v-for="(value, idx) in keyValue"
        :key="value"
        :name="value"
        :id="idx +1"
        class='key'
        @click="setValueOperand(value)">
        {{value}}
      </button>
    </div>
        </div>
        <input type="radio" name="radio" id="one" value="operand1" v-model="picked" checked>
        <label for="one">Число 1</label>
        <br>
        <input type="radio" name="radio" id="two" value="operand2" v-model="picked">
        <label for="two">Число 2</label>
        <br>
        <!-- <span>Выбрано: {{ picked }}</span> -->
        </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    type: String,
             
  },
  data(){
    return{
      msg: "Hello Vue!",
      myCollection: [1,2,3,4,5,6],
      operands: ['+','-','/','*','Степень', 'Int /'],
      operand1: "0",
      operand2: "0",
      result: 0,
      resultFib: 0,
      error:'',
      logs: {},
      checkbox: true,
      picked: 'operand1',
      keyValue: [0,1,2,3,4,5,6,7,8,9,'Del'],
      
    };
  }, 
  methods: {
    calculate(operation = '+') {
      this.error = '';
      switch (operation) {
        case '+':
          this.add();
          break;
        case '-':
          this.substruct();
          break;
        case '/':
          this.divide();
          break;
        case '*':
          this.divide();
          break;
        case 'Степень':
          this.multiply();
          break;
        case 'Int /':
          this.divideP();
          break;
      }
      this.logs[Date.now()] = `${this.operand1}${operation}${this.operand2} = ${this.result}`

    },
    add(){
      this.result = +this.operand1 + +this.operand2;
    },
    substruct(){
      this.result = +this.operand1 - +this.operand2;
    },
    onValidate(){
      console.log('Validation!')
    },
    multiply(){
      if (this.operand2==0){
        alert("степень должна быть больше 0!")
      } else {
        let op = +this.operand1;
        let res = +this.operand1;
        for(let i=1; i<+this.operand2; i++){
          this.operand1 = res * +this.operand1;
          this.result = +this.operand1;
        }
      this.operand1 = +op;
}
    },
    divideP(){
      if (this.operand2==0){
        alert("Делить на 0 нельзя!");
      }
      else {
        this.result = parseInt(+this.operand1 / +this.operand2)
      }
    },
    divide(){
      if (this.operand2==0){
        alert("Делить на 0 нельзя!");
      }
      else {
        this.result = +this.operand1 / +this.operand2;
      }
    },
    setValueOperand(op){
      if(this.picked && this.picked == "operand1" && op !== "Del"){
        // console.log(this.picked)
        this.operand1 += op;
      } else if (this.picked && this.picked == "operand2" && op !== "Del"){
        this.operand2 += op;  
      }  else {
            if(this.picked == "operand1"){
              this.operand1 = this.operand1.substr(0,this.operand1.length - 1)
            } else {
              this.operand2 = this.operand2.substr(0,this.operand2.length - 1)
            }      
      }
    },
    getBtnStatusDisabled(operation){
      if(operation === '/' && this.operand2 === 0) {
        return true
      } else if(operation === 'Int /' && this.operand2 === 0){
        return true
      } else {
        return false
      }
    },    
  }
}
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
.keyboard-w {
  display:flex;
  flex-direction:column;
  align-items:center;
}
.row {
  display:flex;
  align-content:space-around;  
}
.key {
  padding: 10px;  
  height:40px;
  width:40px;
  border: 1px solid black;  
  cursor: pointer;
}
.logs {
  display: flex;
  flex-direction: column;
}
.displayButton {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
