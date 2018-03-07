<template>
  <div class="match-list">
    <cube-scroll
      ref="scroll"
      :data="matchList" 
      :options="options"
      @pulling-down="onPullingDown"
      @pulling-up="onPullingUp">
      <ul>
        <li v-for="(item, index) in matchList" :key="index" class="match-item">
          <div class="left-team">
            <img :src="item.hostLogoUrl" alt="" class="logo">
            <p class="name">{{item.hostTeamName}}</p>
          </div>
          <div class="center">
            <p class="guest" :class="{end : item.isEnd}">{{item.guest}}</p>
            <p class="score">{{item.hostScore}} - {{item.guestScore}}</p>
            <p classs="time">{{item.endTime}}</p>
          </div>
          <div class="right-team">
            <img :src="item.guestLogoUrl" alt="" class="logo">
            <p class="name">{{item.guestTeamName}}</p>
          </div>
        </li>
      </ul>
    </cube-scroll>
  </div>
</template>

<script>
import List from '../common/data/match-list'
export default {
  name: 'match-list',
  data () {
    return {
      matchList: List.list,
      options: {
        scrollbar: {
          fade: true
        },
        pullDownRefresh: {
          threshold: 90,
          stop: 40,
          txt: '刷新成功'
        },
        pullUpLoad: {
          threshold: 100,
          txt: {
            more: '加载成功',
            noMore: '没有更多的数据啦'
          }
        }
      }
    }
  },
  created () {
    this.subscribeDialog = this.$createSubscribeDialog()
  },
  methods: {
    subscribe () {
      this.subscribeDialog.show()
    },
    onPullingDown () {
      setTimeout(() => {
        if (Math.random() > 0.5) {
          for (let index = 5; index > 0; index--) {
            let match = this.matchList[index]
            this.matchList.unshift(match)
          }
        } else {
          this.$refs.scroll.forceUpdate()
        }
      }, 1000)
    },
    onPullingUp () {
      setTimeout(() => {
        if (Math.random() > 0.5) {
          for (let index = 5; index < 10; index++) {
            let match = this.matchList[index]
            this.matchList.push(match)
          }
        } else {
          this.$refs.scroll.forceUpdate()
        }
      }, 1000)
    }
  }
}
</script>

<style lang="stylus">
.match-list
  height: 618px
  background-color: white
  .match-item
    border-bottom: 1px solid #f0f0f1
    padding: 10px 0
    display: flex
    justify-content: space-around
    .left-team,.right-team
      text-align: center
      width: 80px
      img
        display: inline-block
        width: 35px
        height: 35px
        margin-bottom: 4px
      .name 
        font-size: 14px
    .center
      font-size: 12px
      width: 80px
      .guest
        display: inline-block
        background-color: #3D8F29
        color: white
        line-height: 16px
        padding: 3px 10px
        border-radius: 25px
        margin-bottom: 5px
      .end
        background-color: #E86F5D
      .score
        font-size: 14px
        font-weight: 500
        margin-bottom: 5px
</style>
