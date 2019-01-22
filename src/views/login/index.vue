<template>
  <div class="login-container">
    <div class="login-content">
      <div class="login-header">
        <h2 class="login-brand">{{ $t('app.brandname') }}</h2>
      </div>
      <el-form ref="loginForm" :model="loginForm" :rules="loginRules" auto-complete="on" class="login-form" label-position="left" >
        <div class="title-container">
          <h3 class="title">{{ $t('login.title') }}</h3>
          <lang-select class="set-language"/>
        </div>

        <el-form-item prop="username">
          <span class="svg-container">
            <svg-icon icon-class="user"/>
          </span>
          <el-input v-model="loginForm.username" :placeholder="$t('login.username')" auto-complete="on" name="username" type="text" />
        </el-form-item>

        <el-form-item prop="password">
          <span class="svg-container">
            <svg-icon icon-class="password"/>
          </span>
          <el-input
            v-model="loginForm.password"
            :placeholder="$t('login.password')"
            :type="passwordType"
            name="password"
            auto-complete="on"
            @keyup.enter.native="handleLogin"
          />
          <span class="show-pwd" @click="showPwd">
            <svg-icon icon-class="eye"/>
          </span>
        </el-form-item>

        <el-button :loading="loading" class="login-btn" type="primary" @click.native.prevent="handleLogin">{{ $t('login.logIn') }}</el-button>
        <!-- <div style="position:relative">
          <div class="tips">
            <span>{{ $t('login.username') }} : admin</span>
            <span>{{ $t('login.password') }} : {{ $t('login.any') }}</span>
          </div>
          <div class="tips">
            <span style="margin-right:18px;">{{ $t('login.username') }} : editor</span>
            <span>{{ $t('login.password') }} : {{ $t('login.any') }}</span>
          </div>

          <el-button
            class="thirdparty-button"
            type="primary"
            @click="showDialog=true"
          >{{ $t('login.thirdparty') }}</el-button>
        </div>-->
      </el-form>
    </div>
    <div class="login-footer">
      <p>2019 © VR商城</p>
      <p>
        <a href="http://simpleway.com.cn" target="_blank">技术支持 圣卜威科技</a>
      </p>
    </div>
    <el-dialog :title="$t('login.thirdparty')" :visible.sync="showDialog">
      {{ $t('login.thirdpartyTips') }}
      <br>
      <br>
      <br>
      <social-sign/>
    </el-dialog>
  </div>
</template>

<script>
import { isvalidUsername } from '@/utils/validate'
import LangSelect from '@/components/LangSelect'
import SocialSign from './socialsignin'

export default {
  name: 'Login',
  components: { LangSelect, SocialSign },
  data() {
    const validateUsername = (rule, value, callback) => {
      if (!isvalidUsername(value)) {
        callback(new Error('请输入正确的账号'))
      } else {
        callback()
      }
    }
    const validatePassword = (rule, value, callback) => {
      if (value.length < 6) {
        callback(new Error('密码为不小于6位的字符'))
      } else {
        callback()
      }
    }
    return {
      loginForm: {
        username: 'admin',
        password: '1111111'
      },
      loginRules: {
        username: [{ required: true, trigger: 'blur', validator: validateUsername }],
        password: [{ required: true, trigger: 'blur', validator: validatePassword }]
      },
      passwordType: 'password',
      loading: false,
      showDialog: false,
      redirect: undefined
    }
  },
  watch: {
    $route: {
      handler: function(route) {
        this.redirect = route.query && route.query.redirect
      },
      immediate: true
    }
  },
  created() {
    // window.addEventListener('hashchange', this.afterQRScan)
  },
  destroyed() {
    // window.removeEventListener('hashchange', this.afterQRScan)
  },
  methods: {
    showPwd() {
      if (this.passwordType === 'password') {
        this.passwordType = ''
      } else {
        this.passwordType = 'password'
      }
    },
    handleLogin() {
      this.$refs.loginForm.validate(valid => {
        if (valid) {
          this.loading = true
          this.$store
            .dispatch('LoginByUsername', this.loginForm)
            .then(() => {
              this.loading = false
              this.$router.push({ path: this.redirect || '/' })
            })
            .catch(() => {
              this.loading = false
            })
        } else {
          console.log('error submit!!')
          return false
        }
      })
    },
    afterQRScan() {
      // const hash = window.location.hash.slice(1)
      // const hashObj = getQueryObject(hash)
      // const originUrl = window.location.origin
      // history.replaceState({}, '', originUrl)
      // const codeMap = {
      //   wechat: 'code',
      //   tencent: 'code'
      // }
      // const codeName = hashObj[codeMap[this.auth_type]]
      // if (!codeName) {
      //   alert('第三方登录失败')
      // } else {
      //   this.$store.dispatch('LoginByThirdparty', codeName).then(() => {
      //     this.$router.push({ path: '/' })
      //   })
      // }
    }
  }
}
</script>

<style rel="stylesheet/scss" lang="scss">
/* 修复input 背景不协调 和光标变色 */
/* Detail see https://github.com/PanJiaChen/vue-element-admin/pull/927 */

$bg: #ccc;
$light_gray: #606266;
$cursor: #000;

@supports (-webkit-mask: none) and (not (cater-color: $cursor)) {
  .login-container .el-input input {
    color: $cursor;
    &::first-line {
      color: $light_gray;
    }
  }
}

/* reset element-ui css */
.login-container {
  .el-input {
    display: inline-block;
    height: 47px;
    width: 85%;
    input {
      background: transparent;
      border: 0px;
      -webkit-appearance: none;
      border-radius: 0px;
      padding: 12px 5px 12px 15px;
      color: $light_gray;
      height: 47px;
      caret-color: $cursor;
      &:-webkit-autofill {
        -webkit-box-shadow: 0 0 0px 1000px $bg inset !important;
        -webkit-text-fill-color: $cursor !important;
      }
    }
  }
  .el-form-item {
    border: 1px solid rgba(255, 255, 255, 0.1);
    background: rgba(0, 0, 0, 0.1);
    border-radius: 5px;
    color: #454545;
  }
}
</style>

<style rel="stylesheet/scss" lang="scss" scoped>
$bg: #ccc;
$dark_gray: #889aa4;
$light_gray: #606266;

.login-container {
  background-image: url('../../assets/site_images/login_bg_sf.jpg');
  background-size: cover;
  min-height: 100%;
  width: 100%;
  background-color: $bg;
  overflow: hidden;
  .login-content {
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-orient: vertical;
    -webkit-box-direction: normal;
    -ms-flex-flow: column wrap;
    flex-flow: column wrap;
    -webkit-box-pack: center;
    -ms-flex-pack: center;
    justify-content: center;
    -webkit-box-align: center;
    -ms-flex-align: center;
    align-items: center;
    min-height: 100vh;
    padding: 50px 20px 150px;
    text-align: center;

    .login-header {
      padding: 20px;
      color: light_gray;
      .login-brand {
        margin: 0 0 15px;
        font-size: 34px;
        font-weight: 400;
        letter-spacing: 2px;
        text-transform: uppercase;
      }
    }

    .login-form {
      position: relative;
      width: 500px;
      max-width: 100%;
      padding: 20px 35px;
      margin: 0 auto;
      overflow: hidden;
      background: #fff;
      border-radius: 5px;
    }
    .tips {
      font-size: 14px;
      // color: #fff;
      margin-bottom: 10px;
      span {
        &:first-of-type {
          margin-right: 16px;
        }
      }
    }
    .svg-container {
      padding: 6px 5px 6px 15px;
      color: $dark_gray;
      vertical-align: middle;
      width: 30px;
      display: inline-block;
    }
    .title-container {
      position: relative;
      .title {
        font-size: 26px;
        color: $light_gray;
        margin: 0px auto 40px auto;
        text-align: center;
        font-weight: bold;
      }
      .set-language {
        // color: #fff;
        position: absolute;
        top: 5px;
        right: 0px;
      }
    }
    .show-pwd {
      position: absolute;
      right: 10px;
      top: 7px;
      font-size: 16px;
      color: $dark_gray;
      cursor: pointer;
      user-select: none;
    }
    .login-btn {
      width: 100%;
      margin-bottom: 30px;
      font-size: 16px;
      height: 47px;
    }
    .thirdparty-button {
      position: absolute;
      right: 0;
      bottom: 6px;
    }
  }

  .login-footer {
    position: absolute;
    bottom: 0;
    padding: 20px;
    color: hsla(0, 0%, 100%, 0.9);
    width: 100%;
    text-align: center;
    font-size: 14px;
  }
}
</style>
