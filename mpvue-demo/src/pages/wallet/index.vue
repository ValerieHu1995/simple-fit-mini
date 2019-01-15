<template>
  <div class="LayerBottom">
    <i-panel style="margin-top:4rem;" @click="account">
      <div class="card">
        <i-avatar src="https://i.loli.net/2017/08/21/599a521472424.jpg" size="large" shape="square"></i-avatar>
        <div class="card-box">
          <div class="card-info">会员名称</div>
          <div class="card-detial">id:&nbsp;{{23213313323312}}</div>
        </div>
      </div>
    </i-panel>
    <i-panel title="账户余额">
      <div class="money-box">￥{{1342422.00}}</div>
    </i-panel>
    <i-panel title="本月盈利" style="margin-bottom:8.3rem;">
      <div class="money-box">￥{{13422.00}}</div>
    </i-panel>
  </div>
</template>

<script>
import { hostUrl } from "@/utils/index";
export default {
  data() {
    return {
      username: "koon1",
      items: [1, 34, 89, 92, 45, 76, 33]
    };
  },
  methods: {
    account() {
      var url = "../account/main";
      wx.navigateTo({ url });
    }
  },
  onShow() {
    wx.request({
      url: hostUrl + "user/" + this.username + "/info",
      data: {
        username: this.username
      },
      method: "POST",
      header: {
        "content-type": "application/x-www-form-urlencoded"
      },
      success: function(res) {
        console.log("submit success");
      },
      fail: function(res) {
        console.log("submit fail");
      }
    });
    var userdata = wx.getStorageSync("userdata");
    this.usertype = userdata.usertype;
  }
};
</script>

<style scoped>
.money-box {
  padding-top: 1rem;
  padding-bottom: 1rem;
  text-align: center;
}
</style>
