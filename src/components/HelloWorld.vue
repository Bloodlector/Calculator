<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <hr/>
    <!-- <button v-on:click="doThat('hello', $event)">click me</button>
    <button @click="doThat('hello', $event)">click me2</button>
    <input type="text" @blur="onValidate"/> -->
    <div class="display">
      <input v-model="operand1" type="number"><span>Число 1</span>
      <input v-model="operand2" type="number"><span>Число 2</span><br>
      <span>Результат</span>= {{ result }}
    </div>

    <div class="keyboard">
      <button @click='result = +operand1 + +operand2'>+</button>
      <button @click='result = +operand1 - +operand2'>-</button>
      <button @click='divide(operand1, operand2)'>/</button>
      <button @click='result = +operand1 * +operand2'>*</button><br>
      <button @click='multiply(operand1, operand2)'>Степень</button><span> Число 1 возвести в степень равную числу 2</span>
      <button @click='divideP(operand1, operand2)'>Int /</button><span> целочисленное деления числа 1 на число 2</span>
    </div>



  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
    
  },
  data(){
    return{
      message: "Hello Vue!",
      operand1: 0,
      operand2: 0,
      result: 0,
    }
  },
  methods: {
    doThat(str, evnt){
      console.log('click', str, evnt)
    },
    onValidate(){
      console.log('Validation!')
    },
    multiply(){
if (this.operand2==0){
  alert("степень должна быть больше 0!")
} else {
        let op = this.operand1;
      let res = this.operand1;
      for(let i=1; i<this.operand2; i++){
      this.operand1 = res * this.operand1;
      this.result = this.operand1;
      }
      this.operand1 = op;
}
    },
    divideP(){
      if (this.operand2==0){
        alert("Делить на 0 нельзя!");
      }
      else {
      this.result = parseInt(this.operand1 / this.operand2)
      }
    },
        divide(){
      if (this.operand2==0){
        alert("Делить на 0 нельзя!");
      }
      else {
      this.result = this.operand1 / this.operand2;
      }
    }
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
</style>
