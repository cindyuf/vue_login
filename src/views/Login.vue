<template>
  <div class="login-container">
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
          <el-button @click="handleReset" class="reset-btn">重置</el-button>
        </el-form-item>
      </el-form>

      <p class="tip">测试账号: user / password</p>
    </div>
  </div>
</template>

<script>
import { reactive, ref } from 'vue'
import { useStore } from 'vuex'
import { useRouter } from 'vue-router'
import { ElMessage } from 'element-plus'

export default {
  name: 'Login',
  setup() {
    const store = useStore()
    const router = useRouter()
    const loading = ref(false)

    const form = reactive({
      username: '',
      password: ''
    })

    const handleLogin = () => {
      if (!form.username || !form.password) {
        ElMessage.warning('请输入用户名和密码')
        return
      }

      if (form.username === 'user' && form.password === 'password') {
        store.commit('login')
        ElMessage.success('登录成功')
        router.push('/')
      } else {
        ElMessage.error('用户名或密码错误')
      }
    }

    const handleReset = () => {
      form.username = ''
      form.password = ''
      ElMessage.info('表单已重置')
    }

    return {
      form,
      loading,
      handleLogin,
      handleReset
    }
  }
}
</script>

<style scoped>
.login-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
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