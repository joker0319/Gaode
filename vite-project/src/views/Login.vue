<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()
const form = ref({
  username: '',
  password: ''
})

const handleSubmit = () => {
  // TODO: 处理登录逻辑
  console.log('登录信息：', form.value)
}

const goToRegister = () => {
  router.push('/register')
}
</script>

<template>
  <div class="login-container">
    <a-card class="login-card" title="用户登录">
      <a-form :model="form" @submit="handleSubmit">
        <a-form-item field="username" label="用户名">
          <a-input v-model="form.username" placeholder="请输入用户名" />
        </a-form-item>
        <a-form-item field="password" label="密码">
          <a-input-password v-model="form.password" placeholder="请输入密码" />
        </a-form-item>
        <a-form-item>
          <a-space>
            <a-button type="primary" html-type="submit">登录</a-button>
            <a-button type="text" @click="goToRegister">还没有账号？去注册</a-button>
          </a-space>
        </a-form-item>
      </a-form>
    </a-card>
  </div>
</template>

<style scoped>
.login-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
  background-color: var(--color-fill-2);
}

.login-card {
  width: 400px;
  border-radius: 8px;
}
</style> 