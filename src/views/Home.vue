<template>
  <div class="home">
    <!-- 导航栏 -->
    <div class="nav-bar">
      <span class="nav-link active">Home</span> |
      <span class="nav-link">About</span> |
      <span class="nav-link" @click="goToLogin">Login</span>
    </div>

    <!-- 按钮区域 -->
    <div class="button-area">
      <el-button v-if="!isLogin" type="primary" @click="goToLogin">登录</el-button>
      <el-button v-else @click="handleLogout">退出登录</el-button>
    </div>

    <!-- 状态显示 -->
    <div class="status-section">
      <div v-if="isLogin" class="status-box">
        <h3 class="status-title">状态1</h3>
        <p>已经登录!</p>
      </div>

      <div v-else class="status-box">
        <h3 class="status-title">状态2</h3>
        <p>尚未登录，请前往登录页Login</p>
        <p class="status-detail">(点击上方的 login 都可以跳转)</p>
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

.status-section {
  margin-top: 40px;
}

.status-box {
  background: white;
  padding: 20px;
  border-radius: 8px;
  border: 1px solid #ddd;
  text-align: center;
}

.status-title {
  color: #ff6b35;
  font-size: 18px;
  margin-bottom: 15px;
}

.status-detail {
  color: #666;
  font-size: 12px;
  margin-top: 10px;
}
</style>