<template>
  <div class="subscribe-dialog-view">
    <cube-popup ref="popup" @mask-click="hide">
      <div class="subscribe-dialog-wrapper">
        <span class="close" @click="hide"><i class="cubeic-close"></i></span>
        <div class="title">开启推送通知</div>
        <img src="./subscribe.png">
        <p class="desc">第一时间获取最新鲜出炉的新闻攻略、赛事咨询、数据专题、精彩视频</p>
        <cube-button class="button" @click="start">现在开启</cube-button>
      </div>
    </cube-popup>
  </div>
</template>

<script>
export default {
  name: 'subscribe-dialog',
  methods: {
    show () {
      this.$refs.popup.show()
      this.$emit('show')
    },
    hide () {
      this.$refs.popup.hide()
      this.$emit('hide')
    },
    start () {
      this.$refs.popup.hide()
      this.$createToast({
        type: 'correct',
        txt: '开启成功',
        time: 1000
      }).show()
    }
  }
}
</script>

<style lang="stylus">
  .subscribe-dialog-wrapper
    position: relative
    box-sizing: border-box
    max-width: 360px
    margin: 0 25px
    padding: 38px 20px 20px 20px
    background-color: #F6F6F6
    border-radius: 4px
    .close
      position: absolute
      top: 8px
      right: 8px
      font-size: 28px
      color: #A2A8AF
    .title
      font-size: 17px
      color: #222C36
    img
      height: 180px
      margin: 8px 0 5px 0
    .desc
      line-height: 20px
      font-size: 13px
      color: #C0C8D1
    .button
      display: inline-block
      width: 230px
      margin-top: 20px
      padding: 14px
      border-radius: 4px
      font-size: 15px
      background-color: #5B8FDC
</style>

