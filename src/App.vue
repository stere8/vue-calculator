<template>
  <div id="calculator">
    <div class="calculator-screen" ref="calculatorScreen">
      <CalcScreen :data="screenElement"/>
    </div>
  
    <div class="calculator-buttons">
      <div class="row">
        <div class="col-3">
          <CalcButton :character="'1'" :classification="'number'" :action="handleButtonClick()"/>
        </div>
        <div class="col-3">
          <CalcButton :character="'2'" :classification="'number'" :action="handleButtonClick"/>
        </div>
        <div class="col-3">
          <CalcButton :character="'3'" :classification="'number'" :action="handleButtonClick"/>
        </div>
        <div class="col-3">
          <CalcButton :character="'+'" :classification="'operation'" :action="handleButtonClick"/>
        </div>
      </div>
  
      <div class="row">
        <div class="col-3">
          <CalcButton :character="'4'" :classification="'number'" :action="handleButtonClick"/>
        </div>
        <div class="col-3">
          <CalcButton :character="'5'" :classification="'number'" :action="handleButtonClick"/>
        </div>
        <div class="col-3">
          <CalcButton :character="'6'" :classification="'number'" :action="handleButtonClick"/>
        </div>
        <div class="col-3">
          <CalcButton :character="'-'" :classification="'operation'" :action="handleButtonClick"/>
        </div>
      </div>
  
      <div class="row">
        <div class="col-3">
          <CalcButton :character="'7'" :classification="'number'" :action="handleButtonClick"/>
        </div>
        <div class="col-3">
          <CalcButton :character="'8'" :classification="'number'" :action="handleButtonClick"/>
        </div>
        <div class="col-3">
          <CalcButton :character="'9'" :classification="'number'" :action="handleButtonClick"/>
        </div>
        <div class="col-3">
          <CalcButton :character="'/'" :classification="'operation'" :action="handleButtonClick"/>
        </div>
      </div>
  
      <div class="row">
        <div class="col-3">
          <CalcButton :character="'0'" :classification="'operation'" :action="handleButtonClick"/>
        </div>
        <div class="col-3">
          <CalcButton :character="' . '" :classification="'operation'" :action="handleButtonClick"/>
        </div>
        <div class="col-3">
          <CalcButton :character="'*'" :classification="'operation'" :action="handleButtonClick"/>
        </div>
        <div class="col-3">
          <CalcButton :character="'='" :classification="'equals'" :action="handleButtonClick"/>
        </div>
      </div>
    </div>
  </div>
  
</template>

<script>
import CalcButton from './components/calculator-buttons.vue'
import CalcScreen from './components/calculator-screen.vue'
export default {
  name: 'App',
  components: {
    CalcButton,
    CalcScreen
  },
  data(){
    return{
      screenElement : '',
      firstNumber : '',
      secondNumber : '',
      operation :'',
      result : ''
    };
  },    
  methods:{
    handleButtonClick(character, classification) {
      console.log(this.firstNumber,this.operation, this.secondNumber);
  if (classification === 'number') {
    if (character.trim() === '.') {
      // If '.' is pressed as the first character, add '0.' to the screen
      if (this.firstNumber === '') {
        this.firstNumber = '0.';
        this.screenElement = this.firstNumber;
      } else if (!this.firstNumber.includes('.')) {
        // Avoid adding multiple '.' consecutively
        this.firstNumber += character;
        this.screenElement = this.firstNumber;
      }
    } else {
      if(this.operation=== ''){
        this.firstNumber += character;
        this.screenElement = this.firstNumber;
      }
      else{
        this.secondNumber += character;
        this.screenElement = this.secondNumber;
      }
    }
    this.updateDisplay();
  } else if (classification === 'operation') {
     if(this.firstNumber ==='' && this.screenElement === ''){
       this.firstNumber = 0;
       this.screenElement = this.firstNumber;
     }
      // Perform calculations when an operation is pressed
      if (this.firstNumber !== '' && this.operation === '') {
        this.operation = character;
        this.screenElement = this.firstNumber + this.operation;
      } else if (this.firstNumber !== '' && this.operation !== '' && this.secondNumber === '') {
        this.operation = character;
        this.screenElement = this.firstNumber + this.operation;
      } else if (this.firstNumber !== '' && this.operation !== '' && this.secondNumber !== '') {
        this.performCalculations();
        this.operation = character;
        this.screenElement = this.result + this.operation;
        this.firstNumber = this.result.toString();
        this.secondNumber = '';
      
    }this.updateDisplay();
  } else if (classification === 'equals') {
    if (this.firstNumber !== '' && this.operation !== '' && this.secondNumber !== '') {
      this.performCalculations();
      this.screenElement = this.result.toString();
      this.firstNumber = this.result.toString();
      this.secondNumber = '';
      this.operation = '';
    }this.updateDisplay();
  }
}, 
updateDisplay() {
    if (this.operation !== '') {
      this.screenElement = this.firstNumber + ' ' + this.operation + ' ' + this.secondNumber;
      console.log(this.screenElement,1)
    } else {
      this.screenElement = this.firstNumber || this.result; 
      console.log(this.screenElement,2)
    }
  },
  performCalculations() {
  let num1 = parseFloat(this.firstNumber);
  let num2 = parseFloat(this.secondNumber);
  console.log("num1" + num1, "num2"+num2)
  switch (this.operation) {
    case '+':
      return num1 + num2; 
    case '-':
      return num1 - num2;
    case '*':
      return num1 * num2;
    case '/':
      if (num2 === 0) {
        // Handle divide by zero
        return 'Error: Division by zero'; 
      } else {
        return num1 / num2;
      }
    default:
      return 'Error: Invalid operation'; 
  }
}
}}
</script>


<style>
#calculator {
  max-width: 400px;
  margin: 0 auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 10px;
  background-color: #f9f9f9;
}

.calculator-screen {
  margin-bottom: 20px;
}

.calculator-buttons .row {
  margin-bottom: 10px;
}
</style>