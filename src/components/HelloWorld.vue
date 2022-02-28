<template>
  <div class="hello">
    <input v-model.number="first" @focus="onFocusInput('first')">
    <input v-model.number="second" @focus="onFocusInput('second')">

    <div :style="mt">
      <button
          v-for="symbol in symbols"
          :key="symbol"
          @click="handleMath(symbol)"
          :style="buttonStyle"
          :disabled="(symbol == '/' || symbol == '//') && second == 0"
      >
        {{ symbol }}
      </button>
    </div>

    <div :style="mt">Result: {{ result }}</div>

    <div style="margin-top: 100px">
      <input type="checkbox" id="check" :value="false" v-model="isChecked" style="cursor: pointer">
      <label for="check" style="cursor: pointer">Show keyboard</label>

      <div :style="mt" v-show="isChecked">
        <button v-for="num in 10" :key="num" :style="buttonStyle" @click="onClickNum(num - 1)">{{ num - 1 }}</button>
        <button @click="onDeleteNum">← Backspace</button>

        <div :style="mt">
          <input type="radio" id="first" value="first" v-model="radio" style="cursor: pointer">
          <label for="first" style="cursor: pointer">Один</label>
          <input type="radio" id="second" value="second" v-model="radio" style="cursor: pointer">
          <label for="second" style="cursor: pointer">Два</label>
        </div>

      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
      first: 0,
      second: 0,
      result: null,
      isChecked: false,
      symbols: ['+', '-', '*', '/', '//', '**'],
      radio: 'first',
      buttonStyle: {
        marginRight: '5px',
        cursor: 'pointer'
      },
      mt: {
        marginTop: '10px'
      }
    }
  },
  methods: {
    handleMath(operation) {
      const {first, second} = this;
      switch (operation) {
        case '+':
          this.result = first + second;
          break;
        case '-':
          this.result = first - second;
          break;
        case '*':
          this.result = first * second;
          break;
        case '/':
          this.result = first / second;
          break;
        case '//':
          this.result = Math.trunc(first / second);
          break;
        case '**':
          this.result = first ** second;
          break;
      }
    },
    onClickNum(num) {
      this[this.radio] = +`${this[this.radio]}${num}`
    },
    onDeleteNum() {
      let newNumber = [...`${this[this.radio]}`];
      newNumber.length = newNumber.length ? newNumber.length - 1 : newNumber.length;
      this[this.radio] = +newNumber.join('');
    },
    onFocusInput(radio) {
      this.radio = radio;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
