<template>
  <div class="login-page">
    <!-- 导航栏 -->
    <div class="nav-bar">
      <span class="nav-link" @click="goToHome">首页</span> |
      <span class="nav-link active">登录</span>
    </div>

    <!-- 按钮区域 -->
    <div class="button-area">
      <el-button v-if="isLogin" @click="handleLogout" type="danger">退出登录</el-button>
      <el-button v-if="!isLogin" @click="showLoginForm" type="primary">显示登录表单</el-button>
    </div>

    <!-- 登录表单（仅在未登录且显示表单时显示） -->
    <div v-if="!isLogin && showForm" class="login-container">
      <div class="login-card">
        <h2>登录</h2>
        <el-form :model="form">
          <el-form-item label="用户名">
            <el-input v-model="form.username" placeholder="请输入用户名" />
          </el-form-item>
          <el-form-item label="密 码">
            <el-input v-model="form.password" type="password" placeholder="请输入密码" />
          </el-form-item>
          <el-form-item class="button-group">
            <el-button type="primary" @click="handleLogin" class="login-btn">登录</el-button>
          </el-form-item>
        </el-form>
        <p class="tip">测试账号: user / password</p>
      </div>
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
    const showForm = ref(false)

    const form = reactive({
      username: 'user',
      password: 'password'
    })

    const handleLogin = () => {
      if (!form.username || !form.password) {
        ElMessage.warning('请输入用户名和密码')
        return
      }

      if (form.username === 'user' && form.password === 'password') {
        store.commit('login')
        ElMessage.success('登录成功')
        showForm.value = false
      } else {
        ElMessage.error('用户名或密码错误')
      }
    }

    const handleLogout = () => {
      store.commit('logout')
      ElMessage.success('退出登录成功')
    }

    const showLoginForm = () => {
      showForm.value = true
    }

    const goToHome = () => {
      router.push('/')
    }

    return {
      form,
      showForm,
      isLogin,
      handleLogin,
      handleLogout,
      showLoginForm,
      goToHome
    }
  }
}
</script>

<style scoped>
.login-page {
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
  margin-bottom: 40px;
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