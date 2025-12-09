<template>
  <div class="home">

    <div class="welcome-section">
      <h1 class="welcome-title">首页页面</h1>
    </div>

    <div class="nav-bar">
      <span class="nav-link active">首页</span> |
      <span class="nav-link" @click="goToLogin">登录</span>
    </div>

    <div class="button-area">
      <el-button v-if="!isLogin" type="primary" @click="goToLogin">前往登录</el-button>
    </div>

    <div class="status-section">
      <div v-if="isLogin" class="status-box success">
        <h3 class="status-title">状态1 - 已登录</h3>
        <p>欢迎回来！当前处于登录状态</p>
      </div>

      <div v-else class="status-box warning">
        <h3 class="status-title">状态2 - 未登录</h3>
        <p>尚未登录，请先登录系统</p>
      </div>
    </div>
  </div>
</template>

<script>
import { computed } from 'vue'
import { useStore } from 'vuex'
import { useRouter } from 'vue-router'

export default {
  name: 'Home',
  setup() {
    const store = useStore()
    const router = useRouter()

    const isLogin = computed(() => store.getters.isLogin)

    const goToLogin = () => {
      router.push('/login')
    }

    const handleLogout = () => {
      store.commit('logout')
    }

    return {
      isLogin,
      goToLogin,
      handleLogout
    }
  }
}
</script>

<style scoped>
.home {
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

.welcome-section {
  text-align: center;
  margin-bottom: 30px;
}

.welcome-title {
  color: #2c3e50;
  font-size: 28px;
  margin-bottom: 15px;
  font-weight: 600;
}

.welcome-desc {
  color: #666;
  font-size: 16px;
  margin: 0;
}

.button-area {
  text-align: center;
  margin: 20px 0;
}

.button-area .el-button {
  min-width: 100px;
}

.status-section {
  margin-top: 30px;
  width: 100%;
  max-width: 400px;
}

.status-box {
  background: white;
  padding: 25px;
  border-radius: 8px;
  border: 1px solid #ddd;
  text-align: center;
}

.status-box.success {
  border-color: #67c23a;
  background: #f0f9ff;
}

.status-box.warning {
  border-color: #e6a23c;
  background: #fdf6ec;
}

.status-title {
  font-size: 18px;
  margin-bottom: 15px;
  font-weight: 500;
}

.status-box.success .status-title {
  color: #67c23a;
}

.status-box.warning .status-title {
  color: #e6a23c;
}

.status-box p {
  color: #666;
  margin: 0;
  font-size: 14px;
}
</style>