<template>
  <div class="login-page">
    <div class="welcome-section">
      <h1 class="welcome-title">登录页面</h1>
    </div>

    <div class="nav-bar">
      <span class="nav-link" @click="goToHome">首页</span> |
      <span class="nav-link active">登录</span>
    </div>

    <div class="button-area">
      <el-button v-if="isLogin" @click="handleLogout" type="danger">退出登录</el-button>
      <el-button v-if="!isLogin" @click="handleLogin" type="primary">登录</el-button>
    </div>
  </div>
</template>

<script>
import { reactive, ref, computed } from 'vue'
import { useStore } from 'vuex'
import { useRouter } from 'vue-router'
import { ElMessage } from 'element-plus'

export default {
  name: 'Login',
  setup() {
    const store = useStore()
    const router = useRouter()

    const isLogin = computed(() => store.getters.isLogin)

    const form = reactive({
      username: 'user',
      password: 'password'
    })

    const handleLogin = () => {
      store.commit('login')
      ElMessage.success('登录成功')
    }

    const handleLogout = () => {
      store.commit('logout')
      ElMessage.success('退出登录成功')
    }

    const goToHome = () => {
      router.push('/')
    }

    return {
      form,
      isLogin,
      handleLogin,
      handleLogout,
      goToHome
    }
  }
}
</script>

<style scoped>
.login-page {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  padding: 20px;
  max-width: 600px;
  margin: 0 auto;
}

.nav-bar {
  color: #41b883;
  margin-bottom: 20px;
  font-size: 14px;
}

.nav-link {
  cursor: pointer;
  margin: 0 5px;
}

.nav-link.active {
  font-weight: bold;
}

.nav-link:hover {
  text-decoration: underline;
}

.button-area {
  text-align: center;
  margin: 30px 0;
}

.login-container {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 20px;
}

.login-card {
  background: white;
  padding: 30px;
  max-width: 350px;
  width: 100%;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

h2 {
  text-align: center;
  color: #d53f8c;
  margin-bottom: 20px;
}

.button-group {
  text-align: center;
}

.login-btn, .reset-btn {
  width: 80px;
  margin: 0 5px;
}

.tip {
  text-align: center;
  color: #999;
  font-size: 12px;
  margin-top: 15px;
}

:deep(.el-form-item__label) {
  width: 60px !important;
  text-align: justify;
  text-align-last: justify;
}

:deep(.el-form-item__content) {
  margin-left: 10px !important;
  justify-content: center;
}

:deep(.el-input) {
  width: 100%;
}
</style>