<template>
  <div class="LayerBottom">
    <i-panel title="课程信息" style="margin-top:2rem;">
      <div class="card">
        <i-avatar src="https://i.loli.net/2017/08/21/599a521472424.jpg" size="large" shape="square"></i-avatar>
        <div class="card-box">
          <div class="card-info">课程名称</div>
          <div class="card-detial">上课地点:{{220}}</div>
          <div class="card-detial">上课日期:{{"2019-01-12"}}</div>
          <div class="card-detial">上课时间:{{"12:00 - 14:00"}}</div>
        </div>
      </div>
    </i-panel>
    <i-panel title="课程学员" style="margin-bottom:2rem;">
      <div class="card" v-for="item in items">
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
