<template>
  <div class="LayerBottom">
    <i-panel title="添加课程" style="margin-top:2rem;">
      <div style="text-align:center;">
        <i-icon size="60" type="add"/>
      </div>
    </i-panel>
    <i-panel title="课程列表" style="margin-bottom:2rem;">
      <div class="card" v-for="item in items" @click="clickCard">
        <i-avatar src="https://i.loli.net/2017/08/21/599a521472424.jpg"></i-avatar>
        <div class="card-box">
          <div class="card-info">学员名称</div>
        </div>
        <div class="card-box">
          <div class="card-detial">{{"课程名称或卡的名称"}}交易</div>
          <div class="card-detial">交易金额:{{100}}</div>
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
  methods: {
    clickCard({ mp }) {
      console.log(mp._relatedInfo.anchorRelatedText);
      var url = "../billdetial/main";
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
</style>
