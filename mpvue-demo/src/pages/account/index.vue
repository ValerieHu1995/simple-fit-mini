<template>
  <div class="LayerBottom">
    <i-col class="avatar" style="margin-top:2rem;">
      <i-avatar src="https://i.loli.net/2017/08/21/599a521472424.jpg"></i-avatar>
      <dir style="margin-left:5%">{{username}}</dir>
    </i-col>
    <i-panel>
      <i-input :value="username" type="textarea" title="账号" placeholder="请输入用户名" disabled/>
      <i-input :value="userpswd1" type="password" title="密码" placeholder="请输入密码"/>
      <i-input :value="userpswd2" type="password" title="确认密码" placeholder="请再次输入密码"/>
    </i-panel>
    <i-button type="warning" @click="submintUserChangePswd">保存密码</i-button>
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
    submintUserChangePswd() {
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
</style>
