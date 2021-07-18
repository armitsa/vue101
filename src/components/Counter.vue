<template>
  <div class="mb-20">
      Counter: {{number}}
    <div>
        <label for="counter" v-bind:title="number">Counter: </label>
        <input type="text" v-model="number">
      <button v-on:click="increase">+</button>
      <button v-on:click="decrease">-</button>
      <button v-on:click="plus10">+10</button>
      <button v-on:click="multiply2">x2</button>
    </div>
  </div>
</template>

<script>
export default {
    data() {
        return {
            number : 200
        }
    },
    methods: {
        increase() {
            this.number++
        },
        decrease() {
            this.number--
        },
        plus10() {
            this.number = this.number + 10
        },
        multiply2() {
            this.number = this.number*2
        }
    }
}
</script>

<style scoped lang="scss"> 
.mb-20 {
    margin-bottom: 20px;
}
</style>