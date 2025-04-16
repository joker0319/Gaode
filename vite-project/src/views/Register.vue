<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()
const form = ref({
  username: '',
  password: '',
  confirmPassword: '',
  email: ''
})

const handleSubmit = () => {
  // TODO: 处理注册逻辑
  console.log('注册信息：', form.value)
}

const goToLogin = () => {
  router.push('/login')
}
</script>

<template>
  <div class="register-container">
    <a-card class="register-card" title="用户注册">
      <a-form :model="form" @submit="handleSubmit">
        <a-form-item field="username" label="用户名">
          <a-input v-model="form.username" placeholder="请输入用户名" />
        </a-form-item>
        <a-form-item field="email" label="邮箱">
          <a-input v-model="form.email" placeholder="请输入邮箱" />
        </a-form-item>
        <a-form-item field="password" label="密码">
          <a-input-password v-model="form.password" placeholder="请输入密码" />
        </a-form-item>
        <a-form-item field="confirmPassword" label="确认密码">
          <a-input-password v-model="form.confirmPassword" placeholder="请再次输入密码" />
        </a-form-item>
        <a-form-item>
          <a-space>
            <a-button type="primary" html-type="submit">注册</a-button>
            <a-button type="text" @click="goToLogin">已有账号？去登录</a-button>
          </a-space>
        </a-form-item>
      </a-form>
    </a-card>
  </div>
</template>

<style scoped>
.register-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
  background-color: var(--color-fill-2);
}

.register-card {
  width: 400px;
  border-radius: 8px;
}
</style> 