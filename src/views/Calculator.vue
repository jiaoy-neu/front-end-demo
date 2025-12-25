<template>
  <div class="calculator-container">
    <h1>两数相加计算器</h1>
    <input v-model="num1" type="number" placeholder="请输入第一个数字" />
    <input v-model="num2" type="number" placeholder="请输入第二个数字" />
    <button @click="calculate">计算结果</button>
    <p v-if="result !== null">结果: {{ result }}</p>
    <p v-if="error" class="error">{{ error }}</p>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      num1: '',
      num2: '',
      result: null,
      error: ''
    }
  },
  methods: {
    async calculate() {
      this.error = ''
      try {
        const response = await axios.get(`http://localhost:8080/api/demo?a=${parseFloat(this.num1)}&b=${parseFloat(this.num2)}`
        )
        console.log(response, "response")
        this.result = response.data
      } catch (err) {
        this.error = '请求失败，请检查网络或输入'
      }
    }
  }
}
</script>

<style scoped>
.calculator-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 2rem;
  font-family: Arial, sans-serif;
}

input {
  margin: 0.5rem;
  padding: 0.5rem;
  width: 200px;
}

button {
  margin: 1rem;
  padding: 0.5rem 1rem;
  background-color: #42b983;
  color: white;
  border: none;
  cursor: pointer;
  border-radius: 4px;
}

.error {
  color: red;
}
</style>
