<template>
  <div style="height:100%;background-repeat: no-repeat;
    background-size: 100% 100%;" :style="{backgroundImage:'url('+imgSrc+')'}">
    <div class="login_box">
      <!-- 文字描述 -->
      <h3 class="login_title">欢迎登录 Orion Blog</h3>
      <!-- status-icon	是否在输入框中显示校验结果反馈图标	boolean	—	默认为false -->
      <el-form :model="loginForm" status-icon>
        <!-- prop	表单域 model 字段，在使用 validate、resetFields 方法的情况下，该属性是必填的	string	传入 Form 组件的 model 中的字段	— -->
        <el-form-item prop="pass">
          <div class="input_outer">
            <span class="u_user"></span>
            <input v-model="loginForm.userName" type="text" class="login_input" placeholder="请输入账户" />
          </div>
        </el-form-item>
        <el-form-item prop="checkPass">
          <div class="input_outer">
            <span class="us_uer"></span>
            <input type="password" class="login_input" v-model="loginForm.password" placeholder="请输入密码" />
          </div>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" @click="login" class="login_button">登录</el-button>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>

<script>
  import { Message } from 'element-ui'
  export default {
    data() {
      return {
        loginForm: {
          userName: "",
          password: ""
        },
        imgSrc: require('../assets/background.jpg')
      }
    },
    created: function () {
      var _this = this;
      //键盘回车键绑定登录按钮事件
      document.onKeydown = function (e) {
        var key = window.event.keyCode;
        if (key == 13) {
          _this.login();
        }
      }
    },
    methods: {
      //登陆事件
      login() {
        var _this = this;
        if (_this.dataCheck()) {
          //页面跳转
          _this.$router.push("/home");
        }
      },
      //校验数据
      dataCheck() {
        if (!this.loginForm.userName) {
          Message.warning("请输入账号")
          return false;
        }
        if (!this.loginForm.password) {
          Message.warning("请输入密码")
          return false;
        }
        return true;
      }
    }
  }
</script>

<style scoped>
  .login_box {
    width: 315px;
    height: 365px;
    padding: 35px;
    color: #EEE;
    position: absolute;
    left: 50%;
    top: 50%;
    margin-left: -175px;
    margin-top: -200px;
    background: rgba(69, 63, 70, 0.46);
    border-radius: 10px;
  }

  .login_title {
    text-align: center;
    font: 20px "microsoft yahei", Helvetica, Tahoma, Arial, "Microsoft jhengHei", sans-serif;
    color: #FFFFFF;
    height: 15px;
    line-height: 15px;
    padding: 0 0 35px 0;
  }

  .input_outer {
    height: 46px;
    padding: 0 5px;
    margin-bottom: 20px;
    border-radius: 50px;
    position: relative;
    border: rgba(255, 255, 255, 0.2) 2px solid !important;
  }

  .login_input {
    width: 220px;
    height: 46px;
    outline: none;
    display: inline-block;
    font: 14px "microsoft yahei", Helvetica, Tahoma, Arial, "Microsoft jhengHei";
    margin-left: 50px;
    border: none;
    background: none;
    line-height: 46px;
    color: rgb(255, 255, 255) !important;
  }

  .u_user {
    width: 32px;
    height: 32px;
    background: url('../assets/user.png');
    background-repeat: no-repeat;
    /* background-position: -120px 0; */
    position: absolute;
    margin: 7px 2px;
  }

  .us_uer {
    width: 32px;
    height: 32px;
    background-image: url('../assets/password.png');
    background-repeat: no-repeat;
    /* background-position: -125px -34px; */
    position: absolute;
    margin: 7px 2px;
  }

  .login_button {
    border-radius: 50px;
    width: 100%;
  }
</style>