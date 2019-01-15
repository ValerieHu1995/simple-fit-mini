<template>
  <div class="LayerBottom">
    <i-panel style="margin-top:50%">
      <i-input :value="username" type="textarea" title="账号" placeholder="请输入用户名"/>
      <i-input :value="userpswd" type="password" title="密码" placeholder="请输入密码"/>
      <i-radio-group :current="usertype" @change="changeUserType">
        <i-radio value="商家" position="right" color="#ff9900"/>
        <i-radio value="教练" position="right" color="#ff9900"/>
      </i-radio-group>
    </i-panel>
    <i-button type="warning" @click="submintUserLogin">登录</i-button>
    <div class="function">
      <div @click="submintUserSignin">注册账号</div>
      <div @click="submintUserSignin">找回密码</div>
    </div>
  </div>
</template>

<script>
import { hostUrl } from "@/utils/index";
export default {
  data() {
    return {
      username: "koon1",
      userpswd: "czp",
      usertype: "商家"
    };
  },
  methods: {
    changeUserType({ mp }) {
      console.log(mp.detail.value);
      this.usertype = mp.detail.value;
      wx.setStorage({
        key: "userdata",
        data: { usertype: this.usertype },
        success: function() {
          console.log("setStorage success");
        },
        fail: function() {
          console.log("setStorage fail");
        }
      });
    },
    submintUserLogin() {
      wx.request({
        url: hostUrl + "user/" + this.username + "/login",
        data: {
          username: this.username,
          password: this.userpswd
        },
        method: "POST",
        header: {
          "content-type": "application/x-www-form-urlencoded"
        },
        success: function(res) {
          console.log("request success");
          wx.setStorage({
            key: "params",
            data: {
              id: res.data.resObject.id,
              type: res.data.resObject.type
            },
            success: function() {
              console.log("setStorage success");
            },
            fail: function() {
              console.log("setStorage fail");
            }
          });
          var url = "../home/main";
          wx.navigateTo({ url });
        },
        fail: function(res) {
          console.log("request fail");
        },
        complete: function(res) {
          console.log("request complete");
        }
      });
    },
    submintUserSignin() {
      var url = "../signin/main";
      wx.navigateTo({ url });
    }
  },
  onShow() {
    wx.setStorage({
      key: "userdata",
      data: { usertype: this.usertype },
      success: function() {
        console.log("setStorage success");
      },
      fail: function() {
        console.log("setStorage fail");
      }
    });
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
  color: #ff9900;
  font-size: 14px;
}
</style>
