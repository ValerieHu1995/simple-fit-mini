<template>
  <div class="LayerBottom">
    <i-col class="avatar">
      <i-avatar src="https://i.loli.net/2017/08/21/599a521472424.jpg" @click="toggle"></i-avatar>
      <dir @click="selectShop" style="margin-left:5%">{{shopname}}</dir>
    </i-col>
    <i-drawer mode="left" :visible="show" @close="toggle">
      <div class="LayerBottom" style="height:36rem;width:15rem;">
        <i-col class="avatar" style="margin-top:2rem;">
          <i-avatar src="https://i.loli.net/2017/08/21/599a521472424.jpg"></i-avatar>
          <dir style="margin-left:5%">{{username}}</dir>
        </i-col>
        <i-panel>
          <i-grid>
            <i-row>
              <i-grid-item @click="account">
                <i-grid-icon>
                  <i-icon size="30" type="businesscard"/>
                  <i-grid-label>账号</i-grid-label>
                </i-grid-icon>
              </i-grid-item>
              <i-grid-item @click="wallet">
                <i-grid-icon>
                  <i-icon size="30" type="redpacket"/>
                  <i-grid-label>钱包</i-grid-label>
                </i-grid-icon>
              </i-grid-item>
              <i-grid-item v-if="usertype=='商家'">
                <i-grid-icon>
                  <i-icon size="30" type=""/>
                  <i-grid-label></i-grid-label>
                </i-grid-icon>
              </i-grid-item>
              <i-grid-item v-if="usertype=='教练'">
                <i-grid-icon>
                  <i-icon size="30" type="task"/>
                  <i-grid-label>证书</i-grid-label>
                </i-grid-icon>
              </i-grid-item>
            </i-row>
          </i-grid>
        </i-panel>
      </div>
    </i-drawer>
    <i-panel>
      <dataswiper/>
    </i-panel>
    <i-panel v-if="usertype=='商家'" style="margin-top:5%">
      <pictureswiper/>
    </i-panel>
    <i-panel style="margin-top:5%">
      <i-tabs :current="current" color="#ff9900" @change="handleChange">
        <i-tab key="tab1" :title="tabdate1"></i-tab>
        <i-tab key="tab2" :title="tabdate2"></i-tab>
        <i-tab key="tab3" :title="tabdate3"></i-tab>
      </i-tabs>
      <div>
        <scroll-view
          scroll-y
          style="height: 200px;"
          bindscrolltoupper="upper"
          bindscrolltolower="lower"
          v-if="current=='tab1'"
        >
          <div class="card" v-for="item in items1" @click="clickCard">
            <i-avatar
              src="https://i.loli.net/2017/08/21/599a521472424.jpg"
              size="large"
              shape="square"
            ></i-avatar>
            <div class="card-box">
              <div class="card-info">
                <div>{{item}}</div>
                <div>{{current}}</div>
              </div>
              <div class="card-detial">上课教练：{{false}}</div>
              <div class="card-detial">上课地点：{{1+3}}</div>
            </div>
          </div>
        </scroll-view>
        <scroll-view
          scroll-y
          style="height: 200px;"
          bindscrolltoupper="upper"
          bindscrolltolower="lower"
          v-if="current=='tab2'"
        >
          <div class="card" v-for="item in items2" @click="clickCard">
            <i-avatar
              src="https://i.loli.net/2017/08/21/599a521472424.jpg"
              size="large"
              shape="square"
            ></i-avatar>
            <div class="card-box">
              <div class="card-info">
                <div>{{item}}</div>
                <div>{{current}}</div>
              </div>
              <div class="card-detial">上课教练：{{true}}</div>
              <div class="card-detial">上课地点：{{13}}</div>
            </div>
          </div>
        </scroll-view>
        <scroll-view
          scroll-y
          style="height: 200px;"
          bindscrolltoupper="upper"
          bindscrolltolower="lower"
          v-if="current=='tab3'"
        >
          <div class="card" v-for="item in items3" @click="clickCard">
            <i-avatar
              src="https://i.loli.net/2017/08/21/599a521472424.jpg"
              size="large"
              shape="square"
            ></i-avatar>
            <div class="card-box">
              <div class="card-info">
                <div>{{item}}</div>
                <div>{{current}}</div>
              </div>
              <div class="card-detial">上课教练：{{null}}</div>
              <div class="card-detial">上课地点：{{5}}</div>
            </div>
          </div>
        </scroll-view>
      </div>
    </i-panel>
    <i-panel style="margin-top:5%;margin-bottom:5%">
      <i-grid>
        <i-row>
          <i-grid-item @click="scan">
            <i-grid-icon>
              <i-icon size="30" type="scan"/>
              <i-grid-label>扫码</i-grid-label>
            </i-grid-icon>
          </i-grid-item>
          <i-grid-item @click="bill">
            <i-grid-icon>
              <i-icon size="30" type="barrage"/>
              <i-grid-label>账单</i-grid-label>
            </i-grid-icon>
          </i-grid-item>
          <i-grid-item @click="classs">
            <i-grid-icon>
              <i-icon size="30" type="computer"/>
              <i-grid-label>课程</i-grid-label>
            </i-grid-icon>
          </i-grid-item>
        </i-row>
        <i-row>
          <!-- <i-grid-item v-if="usertype=='商家'">
            <i-grid-icon>
              <i-icon size="30" type="addressbook"/>
              <i-grid-label>审批</i-grid-label>
            </i-grid-icon>
          </i-grid-item>
          <i-grid-item v-if="usertype=='教练'">
            <i-grid-icon>
              <i-icon size="30" type="addressbook"/>
              <i-grid-label>申请</i-grid-label>
            </i-grid-icon>
          </i-grid-item>-->

          <i-grid-item @click="list">
            <i-grid-icon>
              <i-icon size="30" type="activity"/>
              <i-grid-label>记录</i-grid-label>
            </i-grid-icon>
          </i-grid-item>
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
        </i-row>
      </i-grid>
    </i-panel>
    <i-panel style="margin-bottom:3.4rem;" v-if="usertype=='教练'"></i-panel>
    <i-action-sheet
      :visible="visible"
      :actions="actions"
      show-cancel
      @cancel="handleCancel"
      @click="handleClickItem"
    />
  </div>
</template>

<script>
import dataswiper from "@/components/dataswiper";
import pictureswiper from "@/components/pictureswiper";
import { hostUrl } from "@/utils/index";

export default {
  data() {
    return {
      show: false,
      tabdate1: "",
      tabdate2: "",
      tabdate3: "",
      current: "tab1",
      shopname: "猪场S",
      username: "koon1",
      usertype: "教练",
      visible: false,
      actions: [
        {
          name: "猪场A"
        },
        {
          name: "猪场B"
        },
        {
          name: "猪场C"
        }
      ],
      items1: [1, 34, 89, 92, 45, 76, 33],
      items2: [45, 76, 33],
      items3: [1, 34, 89, 92]
    };
  },

  components: {
    dataswiper,
    pictureswiper
  },
  methods: {
    toggle() {
      this.show = !this.show;
    },
    handleChange({ target }) {
      console.log(target.key);
      this.current = target.key;
    },
    selectShop() {
      this.visible = true;
    },
    handleCancel() {
      this.visible = false;
    },
    handleClickItem({ mp }) {
      console.log(mp._relatedInfo.anchorTargetText);
    },
    account() {
      var url = "../account/main";
      wx.navigateTo({ url });
    },
    wallet() {
      var url = "../wallet/main";
      wx.navigateTo({ url });
    },
    clickCard({ mp }) {
      console.log(mp._relatedInfo.anchorRelatedText);
      var url = "../timetable/main";
      wx.navigateTo({ url });
    },
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
    bill() {
      var url = "../bill/main";
      wx.navigateTo({ url });
    },
    classs() {
      var url = "../classs/main";
      wx.navigateTo({ url });
    },
    list(){
      var url = "../list/main";
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
    var date = new Date();
    this.tabdate1 = date.getMonth() + 1 + "月" + (date.getDate() + 0) + "日";
    this.tabdate2 = date.getMonth() + 1 + "月" + (date.getDate() + 1) + "日";
    this.tabdate3 = date.getMonth() + 1 + "月" + (date.getDate() + 2) + "日";
    var userdata = wx.getStorageSync("userdata");
    this.usertype = userdata.usertype;
  }
};
</script>

<style scoped>
.card {
  background-color: #ffffff;
  border-radius: 10px;
}
</style>
