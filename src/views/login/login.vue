<template>
  <el-form
    v-loading="loading"
    element-loading-text="正在登录..."
    element-loading-spinner="el-icon-loading"
    element-loading-background="rgba(0, 0, 0, 0.8)"
    :rules="rules"
    :model="loginForm"
    class="loginContainer"
    ref="loginForm"
  >
    <h1 class="loginTitle">博客登录</h1>
    <el-form-item prop="username">
      <el-input
        type="text"
        placeholder="请输入手机号"
        required="required"
        v-model="loginForm.username"
        auto-complete="off"
        @keyup.enter.native="submitLogin"
      ></el-input>
    </el-form-item>
    <el-form-item prop="password">
      <el-input
        type="password"
        placeholder="请输入密码"
        auto-complete="off"
        v-model="loginForm.password"
        @keyup.enter.native="submitLogin"
      ></el-input>
    </el-form-item>
    <el-form-item>
      <el-button type="primary" @click="submitLogin">登录</el-button>
	  <el-button type="primary" @click="toRegister">去注册</el-button>
    </el-form-item>
  </el-form>
</template>

<script>
export default {
  name: "Login",
  data() {
    return {
      loginForm: {
        username: "",
        password: "",
      },
      checked: true,
      rules: {
        //required:true:用户名必填  如果没填就弹出““””“"请输入用户名",trigger:blur 触发的方式是blur
        username: [
          { required: true, message: "手机号不能为空", trigger: "blur" },
        ],
        password: [
          { required: true, message: "密码不能为空", trigger: "blur" },
        ],
      },
      loading: false, //加载样式
    };
  },
  methods: {
    submitLogin() {
      this.$refs.loginForm.validate((validate) => {
        // Element自带的校验
        if (validate) {
           this.axios
            .post(
              "/user/login?username=" +
                this.loginForm.username +
                "&password=" +
                this.loginForm.password
            )
            .then((resp) => {
              console.log(resp.data);
              window.sessionStorage.setItem("user", JSON.stringify(resp.data));
              console.log(JSON.stringify(resp.data))
              this.$router.replace("/home");
            });
        } else {
          this.$message.error("请输入所有字段");
          return false;
        }
      });
    },
    toRegister() {
      this.$router.replace("/register");
    },
  },
};
</script>
 
<style scoped>
.loginContainer {
  border-radius: 15px;
  background-clip: padding-box;
  margin: 180px auto;
  width: 350px;
  padding: 15px 35px 15px 35px;
  background: #fff;
  border: 1px solid #eaeaea;
  box-shadow: 0 0 25px #cac6c6;
}
.loginTitle {
  margin: 15px auto 20px auto;
  text-align: center;
  color: #505458;
}
</style>