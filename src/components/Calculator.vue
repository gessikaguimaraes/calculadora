<template>
  <div class="p-3 rounded calc">
    <!-- Resultado -->
    <div class="w-full rounded m-1 p-3 text-end lead font-weight-bold text-white bg-vue-dark">
      <div>
        {{ calculatorHistory || 0 }}
      </div>
      <div>
        <hr />
      </div>
      <div>
        {{ calculatorValue || 0 }}
      </div>
    </div>
    <!-- Buttons -->
    <div class="row g-0">
      <div class="col-3" v-for="n in calculatorElements" :key="n">
        <div class="lead text-white text-center m-1 py-3 bg-vue-dark rounded hover-class"
          :class="{ 'bg-vue-pink': ['C', '*', '/', '-', '+', '%', '='].includes(n) }" @click="action(n)">
          {{ n }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'CalculadoraBasica',
  props: {
    msg: String
  },
  data() {
    return {
      calculatorValue: '',
      calculatorHistory: '',
      calculatorElements: ['C', '*', '/', '-', 7, 8, 9, '+', 4, 5, 6, '%', 1, 2, 3, '=', 0, '.'],
      operator: null,
      previousCalculatorValue: '',
      porcentagem: null
    }
  },
  methods: {
    action(n) {
      //Acrescentar Valor
      if (!isNaN(n) || n === '.') {
        this.calculatorValue += n + '';
      }

      if (n !== '/' && n != '*' && n != '-' && n != '+' && n != '%' && n != 'C' && n != '=' && n != '.') {
        this.valor = n;
      }

      //Limpar Valor
      if (n === 'C') {
        this.calculatorValue = '';
        this.calculatorHistory = '';
      }

      //Porcentagem
      if (n === "%") {
        this.porcentagem = n;
        // if (this.valor !== '') {
        //   console.info(125);
        // }
        // this.valor = this.valor / 100 + '';
        // console.info(this.calculatorValue.length);
        this.calculatorValue += n + '';
      }

      if (['/', '*', '-', '+'].includes(n)) {
        this.operator = n;
        this.previousCalculatorValue = this.calculatorValue;
        this.calculatorValue += n;
      }

      if (n === '=') {
        this.calculatorHistory = this.previousCalculatorValue + this.operator + this.valor;
        if (this.porcentagem != null) {
          console.info(this.calculatorValue)
        }
        this.calculatorValue = eval(
          this.previousCalculatorValue + this.operator + this.valor
        );
        this.previousCalculatorValue = '';
        this.operator = null;
        this.valor = '';

      }
    }
  }
}
</script>

<style scoped>
.calc {
  max-width: 400px;
  margin: 50px auto;
  /* background: #234; */
  background: #fdf4f9;
  border: #31475e solid 2px;
  box-shadow: 3px 3px 5px #31475e;
}

.bg-vue-dark {
  background: #0b0b0b;
}

.hover-class:hover {
  cursor: pointer;
  background: #305875;
}

.bg-vue-green {
  background: #3fb984;
}

.bg-vue-pink {
  background: #f1047b;
}
</style>
