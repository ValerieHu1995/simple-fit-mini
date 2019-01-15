<template>
  <div class="LayerBottom">
    <i-col class="avatar">
      <i-avatar src="https://i.loli.net/2017/08/21/599a521472424.jpg" @click="toggle"></i-avatar>
      <dir @click="selectShop" style="margin-left:5%">{{username}}</dir>
    </i-col>
    <i-panel>
      <div class="bar">
        <img src="https://i.loli.net/2017/08/21/599a521472424.jpg" alt="icon">
        <input type="text" placeholder="点击搜索您需要的信息">
      </div>
    </i-panel>
    <i-panel style="margin-top:1rem;margin-bottom:1rem;">
      <scroll-view
        scroll-y
        style="height:30rem;"
        bindscrolltoupper="upper"
        bindscrolltolower="lower"
      >
        <div class="card" v-for="item in items" @click="clickCard">
          <i-avatar
            src="https://i.loli.net/2017/08/21/599a521472424.jpg"
            size="large"
            shape="square"
          ></i-avatar>
          <div class="card-box">
            <div class="card-info">
              <div>门店名称</div>
              <div>课程时间</div>
            </div>
            <div class="card-detial">上课教练：{{false}}</div>
            <div class="card-detial">上课地点：{{1+3}}</div>
          </div>
        </div>
      </scroll-view>
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
    scan() {
      wx.scanCode({
        success: function(res) {
          console.log("scanCode success");
        },
        fail: function(res) {
          console.log("scanCode fail");
        }
      });
    },
    clickCard({ mp }) {
      console.log(mp._relatedInfo.anchorRelatedText);
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
  border-radius: 0.1rem;
  background-color: #ffffff;
  display: flex;
  flex-direction: row;
}
.card-box {
  margin: 0rem 0rem 0rem 0.2rem;
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
  color: #2d8cf0;
  font-size: 14px;
}
::-webkit-scrollbar {
  width: 0;
  height: 0;
  color: transparent;
}
</style>
