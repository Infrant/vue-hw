<template>
  <div class="hello">
    <input v-model.number="first">
    <input v-model.number="second">
    <div>
      <button @click="handleMath('sum')">+</button>
      <button @click="handleMath('dif')">-</button>
      <button @click="handleMath('mult')">*</button>
      <button @click="handleMath('divide')" :disabled="second == 0">/</button>
      <button @click="handleMath('divideByInt')" :disabled="second == 0">÷</button>
      <button @click="handleMath('pow')">**</button>
    </div>
    <div>Результат: {{ result }}</div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
      first: 0,
      second: 0,
      result: null
    }
  },
  methods: {
    handleMath(operation) {
      const {first, second} = this;
      switch (operation) {
        case 'sum':
          this.result = first + second;
          break;
        case 'dif':
          this.result = first - second;
          break;
        case 'mult':
          this.result = first * second;
          break;
        case 'divide':
          this.result = first / second;
          break;
        case 'divideByInt':
          this.result = Math.trunc(first / second);
          break;
        case 'pow':
          this.result = first ** second;
          break;
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
