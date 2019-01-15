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
::-webkit-scrollbar {
  width: 0;
  height: 0;
  color: transparent;
}
.LayerBottom {
  background: -webkit-gradient(
    linear,
    0% 0%,
    0% 100%,
    from(#eeab1c),
    color-stop(0.25, #f4c715),
    to(#feb61f)
  );
  height: 100%;
  display: flex;
  flex-direction: column;
  box-sizing: border-box;
}
.avatar {
  margin-top: 7%;
  margin-left: 5%;
  margin-bottom: 5%;
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
