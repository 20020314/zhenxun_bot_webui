<template>
  <div style="height:100vh;min-height: 500px;">
    <el-header class="homeHeader">
        <div class="title">小真寻的后台捏</div>
        <router-link class="to-myapi" :to="{ name: 'MyApi'}">修改api地址</router-link>
    </el-header>
    <el-form
      @submit.native.prevent
      v-loading="loading"
      element-loading-text="正在登录..."
      element-loading-spinner="el-icon-loading"
      element-loading-background="rgba(0, 0, 0, 0.8)"
      :rules="rules"
      ref="loginForm"
      :model="loginForm"
      class="loginContainer"
    >
      <h3 class="loginTitle">真寻的后台</h3>
      <el-form-item prop="username">
        <el-input
          type="text"
          v-model="loginForm.username"
          placeholder="请输入用户名"
        ></el-input>
      </el-form-item>
      <el-form-item prop="password">
        <el-input
          type="password"
          v-model="loginForm.password"
          placeholder="请输入密码"
        ></el-input>
        <!-- 关闭输入密码在打开时默认获取焦点 -->
      </el-form-item>
      <el-button type="primary" style="width: 100%" native-type="submit" @click="submitLogin"
        >登录</el-button
      >
    </el-form>
  </div>
</template>

<script>
import qs from "qs";
// 导入cookie的获取和设置方法
import { setCookie , clearCookie , getCookie , verifyIdentity} from "@/utils/api";

export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Login",
  created(){//进入登录页面先验证是否已经登录
    verifyIdentity();
  },
  data() {
    return {
      loginForm: {
        username: "",
        password: "",
      },
      rules: {
        username: [
          { required: true, message: "请输入用户名", trigger: "blur" },
        ],
        password: [{ required: true, message: "请输入密码", trigger: "blur" }],
      },
      loading: false,
    };
  },
  methods: {
    submitLogin() {
      this.$refs.loginForm.validate((valid) => {
        if (valid) {
          this.loading = true;
          this.postRequest(
            "/webui/login",
            qs.stringify({
              username: this.loginForm.username,
              password: this.loginForm.password,
            }),
            { headers: { "Content-Type": "application/x-www-form-urlencoded" } }
          ).then((resp) => {
            if (resp) {
              // this.loading = false;
              const tokenStr = resp.token_type + " " + resp.access_token;
              if(getCookie){
                clearCookie("tokenStr");
              }
              setCookie("tokenStr", tokenStr);
              // // 页面跳转
              let path = this.$route.query.redirect;
              this.$router.replace(
                path == "/" || path == undefined ? "/home" : path
              );
            }
          });
        } else {
          this.$message.error("请输入所有字段！");
          return false;
        }
        this.loading = false;
      });
    },
  },
};
</script>

<style>
.homeHeader {
  background-color: #409eff;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0px 15px;
  box-sizing: border-box;
}
.loginContainer {
  position: relative;
  top: calc(50% - 200px);
  border-radius: 15px;
  background-clip: padding-box;
  margin: 0 auto;
  width: 350px;
  padding: 15px 35px 15px 35px;
  background: #fff;
  border: 1px solid #eaeaea;
  box-shadow: 0 0 25px #caca6c;
}
.loginTitle {
  margin: 10px auto 40px auto;
  text-align: center;
}

.loginRemember {
  text-align: left;
  margin: 0px 0px 15px 0px;
}

.el-form-item__content {
  display: flex;
  align-items: center;
}
.to-myapi{
  width: 10rem;
  height: 30px;
  line-height: 30px;
  font-size: 1.2rem;
  color: #FFF;
  text-decoration: none;
  border-radius:100px;
  border: 5px solid #FFF;
}
@media screen  and (max-width:600px) {
  .title{font-size: 1.6rem !important;}
  .loginContainer {width: calc(100vw - 10rem);top: calc(30%);}
  .to-myapi{width: 8rem !important; font-size: 1rem !important;border: 3px solid #FFF !important;}
}
</style>