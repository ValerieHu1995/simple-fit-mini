<script>
export default {
  created() {
    // 调用API从本地缓存中获取数据
    const logs = wx.getStorageSync("logs") || [];
    logs.unshift(Date.now());
    wx.setStorageSync("logs", logs);

    console.log("app created and cache logs by setStorageSync");
  }
};
</script>

<style>
.LayerBottom {
  background: -webkit-linear-gradient(left top, #eeca4d, #adeaf1);
  height: 100%;
  display: flex;
  flex-direction: column;
  box-sizing: border-box;
}
</style>
