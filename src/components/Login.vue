<template>
  <body id="login-body">
    <el-form class="login-container" label-position="left" label-width="0px">
      <h3 class="login-title">系统登陆</h3>
      <el-form-item>
        <el-input type="text" v-model="loginForm.username" auto-complete="off" placeholder="账号"></el-input>
      </el-form-item>
      <el-form-item>
        <el-input type="password" v-model="loginForm.password" auto-complete="off" placeholder="密码"></el-input>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" style="width: 100%;background: #505458; border: none;" v-on:click="login">登录</el-button>
      </el-form-item>
    </el-form>
  </body>
</template>

<script>

export default {
  name: 'Login',
  data () {
    return {
      loginForm: {
        username: '',
        password: ''
      },
      responseResult: []
    }
  },
  methods: {
    login () {
      this.axios({
        method: 'post',
        url: '/api/login',
        data: {
          username: this.loginForm.username,
          password: this.loginForm.password
        }
      })
        .then(successResponse => {
          if (successResponse.data.code === 200) {
            this.$router.replace({path: '/index'})
          }
        })
        .catch(failResponse => {
        })
    }
  }
}
</script>

<style>
  .login-container {
    border-radius: 15px;
    margin: 90px auto;
    width: 350px;
    padding: 35px 35px 15px 35px;
    background: #fff;
    border: 1px solid #eaeaea;
    box-shadow: 0 0 25px #cac6c6;
  }
  
  .login-title {
    margin: 0 auto 40px auto;
    text-align: center;
    color: #505458;
  }

  #login-body {
    background: url("../assets/login.jpg") no-repeat right;
    height: 100%;
    width: 100%;
    background-size: 60%;
    position: fixed;
  }

  /*为了覆盖掉浏览器（用户代理）的默认样式*/
  body {
    margin: 0;
  }
</style>
