<template>
  <div class="LayerBottom">
    <i-panel style="margin-top:4rem;" @click="account">
      <div class="card">
        <i-avatar src="https://i.loli.net/2017/08/21/599a521472424.jpg" size="large" shape="square"></i-avatar>
        <div class="card-box">
          <div class="card-info">会员名称</div>
          <div class="card-detial">id:&nbsp;{{23213313323312}}</div>
          <div class="card-detial">exp:&nbsp;{{"2019.10.19"}}</div>
        </div>
        <i-icon size="30" type="enter"/>
      </div>
    </i-panel>
    <i-panel style="margin-top:1rem;margin-bottom:13.5rem;">
      <i-grid>
        <i-grid-item @click="scan">
          <i-grid-icon>
            <i-icon size="30" type="commodity"/>
            <i-grid-label>订单</i-grid-label>
          </i-grid-icon>
        </i-grid-item>
        <i-grid-item>
          <i-grid-icon>
            <i-icon size="30" type="activity"/>
            <i-grid-label>记录</i-grid-label>
          </i-grid-icon>
        </i-grid-item>
        <i-grid-item>
          <i-grid-icon>
            <i-icon size="30" type="coupons"/>
            <i-grid-label>课表</i-grid-label>
          </i-grid-icon>
        </i-grid-item>
      </i-grid>
      <i-grid>
        <i-grid-item>
          <i-grid-icon>
            <i-icon size="30" type="more"/>
            <i-grid-label>更多</i-grid-label>
          </i-grid-icon>
        </i-grid-item>
        <i-grid-item>
          <i-grid-icon>
            <i-icon size="30" type=""/>
            <i-grid-label></i-grid-label>
          </i-grid-icon>
        </i-grid-item>
        <i-grid-item>
          <i-grid-icon>
            <i-icon size="30" type=""/>
            <i-grid-label></i-grid-label>
          </i-grid-icon>
        </i-grid-item>
      </i-grid>
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
.avatar {
  margin-top: 7%;
  margin-left: 5%;
  margin-bottom: 5%;
}
.bar {
  display: flex;
  flex-direction: row;
}
.bar img {
  height: 0.5rem;
  width: 0.5rem;
  margin: 0.2rem 0.2rem 0.2rem 0.2rem;
}
.bar input {
  text-align: start;
  font-size: 14px;
  border: none;
  background: none;
  margin: 0.2rem 0.2rem 0.2rem 0.2rem;
}
.bar input:focus {
  outline: none;
}
.card {
  margin: 0.1rem 0.2rem 0.1rem 0.2rem;
  padding: 0.2rem 0rem 0.2rem 0.2rem;
  display: flex;
  flex-direction: row;
  align-items: center;
}
.card-box {
  margin: 0rem 0.2rem 0rem 0.2rem;
  width: 80%;
  display: flex;
  flex-direction: column;
}
.card-info {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}
.card-detial {
  color: #cccccc;
  font-size: 14px;
}
</style>
