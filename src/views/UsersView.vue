<template>
  <div class="users">
    <h1>用户列表</h1>
    <div v-if="loading" class="loading">加载中...</div>
    <div v-else-if="error" class="error">{{ error }}</div>
    <div v-else class="user-list">
      <div v-for="user in users" :key="user.id" class="user-card">
        <h3>{{ user.name }}</h3>
        <p>{{ user.email }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'UsersView',
  data() {
    return {
      users: [],
      loading: false,
      error: null
    }
  },
  async mounted() {
    this.loading = true
    try {
      // 使用JSONPlaceholder API获取示例用户数据
      const response = await axios.get('https://jsonplaceholder.typicode.com/users')
      this.users = response.data
    } catch (err) {
      this.error = '获取用户数据失败'
      console.error(err)
    } finally {
      this.loading = false
    }
  }
}
</script>

<style scoped>
.users {
  padding: 20px;
}

.loading,
.error {
  text-align: center;
  padding: 20px;
}

.error {
  color: #e74c3c;
}

.user-list {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 20px;
  margin-top: 20px;
}

.user-card {
  background: #ffffff;
  border: 1px solid #e1e8ed;
  border-radius: 8px;
  padding: 20px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.05);
  transition: transform 0.2s, box-shadow 0.2s;
}

.user-card:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}
</style>
