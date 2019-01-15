<template>
  <div class="LayerBottom">
    <i-panel style="margin-top:50%">
      <i-input :value="username" type="textarea" title="账号" placeholder="请输入用户名"/>
      <i-input :value="userpswd" type="password" title="密码" placeholder="请输入密码"/>
      <i-radio-group :current="usertype" @change="changeUserType">
        <i-radio value="商家" position="right" color="#2d8cf0"/>
        <i-radio value="教练" position="right" color="#2d8cf0"/>
      </i-radio-group>
    </i-panel>
    <i-button type="primary" @click="submintUserSignin">注册</i-button>
    <div class="function">
      <div @click="submintUserLogin">登录账号</div>
      <div @click="submintUserLogin">找回密码</div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      username: "",
      userpswd: "",
      usertype: "商家"
    };
  },
  methods: {
    changeUserType({ mp }) {
      this.usertype = mp.detail.value;
    },
    submintUserLogin() {
      var url = "../login/main";
      wx.navigateTo({ url });
    },
    submintUserSignin() {
      console.log(this);
    }
  }
};
</script>

<style scoped>
.function {
  display: flex;
  justify-content: space-between;
  margin: 0rem 0.2rem 4.2rem 0.2rem;
}
.function div {
  color: #2d8cf0;
  font-size: 14px;
}
</style>