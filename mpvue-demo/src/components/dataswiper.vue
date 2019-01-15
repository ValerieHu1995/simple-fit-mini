<template>
  <swiper style="height:3rem;">
    <swiper-item>
      <div class="md-layout">
        <div class="md-layout-item">
          <div>{{DataDetial[0].num}}</div>
          <div>{{DataDetial[0].name}}</div>
        </div>
        <div class="md-layout-item">
          <div>{{DataDetial[1].num}}</div>
          <div>{{DataDetial[1].name}}</div>
        </div>
      </div>
    </swiper-item>
    <swiper-item>
      <div class="md-layout">
        <div class="md-layout-item">
          <div>{{DataDetial[2].num}}</div>
          <div>{{DataDetial[2].name}}</div>
        </div>
        <div class="md-layout-item">
          <div>{{DataDetial[3].num}}</div>
          <div>{{DataDetial[3].name}}</div>
        </div>
      </div>
    </swiper-item>
  </swiper>
</template>

<script>
export default {
  data() {
    return {
      DataDetial: [
        {
          name: "今日买课",
          num: 0
        },
        {
          name: "今日买卡",
          num: 0
        },
        {
          name: "全部买课",
          num: 0
        },
        {
          name: "全部买卡",
          num: 0
        }
      ]
    };
  },
  created() {
    this.DataDetial[0].num = 100;
    this.DataDetial[1].num = 100;
    this.DataDetial[2].num = 2000;
    this.DataDetial[3].num = 20;
  }
};
</script>

<style>
.md-layout {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
}
.md-layout-item {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
