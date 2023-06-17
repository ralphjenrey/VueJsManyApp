<template>
  <div class="wrapper">
 <div class="calculator card">

  <input type="text" class="calculator-screen z-depth-1" v-model="current" disabled />

  <div class="calculator-keys">

    <button type="button" class="operator btn btn-info" value="+" @click="handleInput">+</button>
    <button type="button" class="operator btn btn-info" value="-" @click="handleInput">-</button>
    <button type="button" class="operator btn btn-info" value="*" @click="handleInput">&times;</button>
    <button type="button" class="operator btn btn-info" value="/" @click="handleInput">&divide;</button>

    <button type="button" value="7" class="btn btn-light waves-effect" @click="handleInput">7</button>
    <button type="button" value="8" class="btn btn-light waves-effect" @click="handleInput">8</button>
    <button type="button" value="9" class="btn btn-light waves-effect" @click="handleInput">9</button>


    <button type="button" value="4" class="btn btn-light waves-effect" @click="handleInput">4</button>
    <button type="button" value="5" class="btn btn-light waves-effect" @click="handleInput">5</button>
    <button type="button" value="6" class="btn btn-light waves-effect" @click="handleInput">6</button>


    
    <button type="button" value="1" class="btn btn-light waves-effect" @click="handleInput">1</button>
    <button type="button" value="2" class="btn btn-light waves-effect" @click="handleInput">2</button>
    <button type="button" value="3" class="btn btn-light waves-effect" @click="handleInput">3</button>


    <button type="button" value="0" class="btn btn-light waves-effect" @click="handleInput">0</button>
    <button type="button" class="decimal function btn btn-secondary" value="." @click="handleInput">.</button>
    <button type="button" class="all-clear function btn btn-danger btn-sm" value="all-clear" @click="clear">AC</button>

    <button type="button" class="equal-sign operator btn btn-default" value="=" @click="calculate">=</button>

  </div>
</div>
    </div>
</template>

<script>
  export default {
  data() {
    return {
      current: "", // Initial value
    };
  },
  methods: {
    handleInput(value) {
       // this.current = Number(this.current);
      if(this.current == 0){
        this.current = event.target.value;
      }
      else{
        this.current += event.target.value;
        if(event.target.value == "+" || event.target.value == "-" || event.target.value == "*" || event.target.value == "/"){
          this.operator = event.target.value;
          this.previous = this.current;
          this.current = "";
        }
      }
       
    },
    clear(){
      this.current = 0;
      this.previous = 0;
      this.opeartion = 0;
    },
    calculate() {
      const a = parseFloat(this.previous);
      const b = parseFloat(this.current);

      if (isNaN(a) || isNaN(b)) {
        return;
      }

      let result = 0;

      switch (this.operator) {
        case "+":
          result = a + b;
          break;
        case "-":
          result = a - b;
          break;
        case "*":
          result = a * b;
          break;
        case "/":
          result = a / b;
          break;
        default:
          return;
      }

      this.current = result.toString();
      this.operator = null;
      this.previous = null;
    },
  },
};
</script>

<style scoped>

  .wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
html {
  font-size: 62.5%;
  box-sizing: border-box;
}

*,
*::before,
*::after {
  margin: 0;
  padding: 0;
  box-sizing: inherit;
}

.calculator {
  border: 1px solid #ccc;
  border-radius: 5px;
  width: 400px;
}

.calculator-screen {
  width: 100%;
  height: 80px;
  border: none;
  background-color: #252525;
  color: #fff;
  text-align: right;
  padding-right: 20px;
  padding-left: 10px;
  font-size: 4rem;
}

button {
  height: 60px;
  font-size: 2rem!important;
}

.equal-sign {
  height: 98%;
  grid-area: 2 / 4 / 6 / 5;
}

.calculator-keys {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-gap: 20px;
  padding: 20px;
}
</style>
