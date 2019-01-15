<template>
  <div class="LayerBottom">
    <i-panel title="交易信息" style="margin-top:2rem;">
      <div class="card">
        <div class="card-box">
          <div class="card-info">{{"课程名称或卡的名称"}}交易</div>
          <div class="card-detial">交易单号:{{213142443355787654324}}</div>
          <div class="card-detial">交易金额:{{100}}</div>
          <div class="card-detial">交易地点:{{220}}</div>
          <div class="card-detial">交易日期:{{"2019-01-12"}}</div>
          <div class="card-detial">交易时间:{{"12:00 - 14:00"}}</div>
        </div>
      </div>
    </i-panel>
    <i-panel title="卖家信息" style="margin-bottom:18rem;">
      <div class="card">
        <i-avatar src="https://i.loli.net/2017/08/21/599a521472424.jpg"></i-avatar>
        <div class="card-box">
          <div class="card-info">学员名称</div>
          <div class="card-detial">学员电话:{{13165988773}}</div>
        </div>
      </div>
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
  methods: {},
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
</style>
