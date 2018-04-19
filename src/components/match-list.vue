<template>
  <div class="match-list">
    <cube-scroll
      ref="scroll"
      :data="matchList" 
      :options="options"
      @pulling-down="onPullingDown"
      @pulling-up="onPullingUp">
      <ul class="match-inner">
        <li v-for="(item, index) in matchList" :key="index" class="match-item" @click="clickItem(item)">
          <div class="left-team">
            <img :src="item.hostLogoUrl" alt="" class="logo">
            <p class="name">{{item.hostTeamName}}</p>
          </div>
          <div class="center">
            <p v-if="item.live" class="guest" :class="{end : item.isEnd}">{{item.live}}</p>
            <p v-if="item.order" class="order" @click="subscribe">{{item.order}}</p>
            <p class="score" :class="{last: item.isEnd}">
              {{item.hostScore}} - {{item.guestScore}}
            </p>
            <p v-if="!item.isEnd" class="time">{{item.endTime}}</p>

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
import { ENDED, LIVE, CONCERN } from '../common/config/tabs'
import list from '../common/data/match-list'
const UP = 'up'
const DOWN = 'down'
const typesMap = {
  [ENDED]: 0,
  [LIVE]: 1,
  [CONCERN]: 2
}
// 处理数据
const getMatchList = (source, type) => {
  return list[source][typesMap[type]]
}

export default {
  name: 'match-list',
  props: {
    source: {
      type: String,
      default: 'soccer'
    },
    type: {
      type: String,
      default: LIVE
    }
  },
  data () {
    return {
      matchList: getMatchList(this.source, this.type),
      options: {
        scrollbar: {
          fade: true
        },
        pullDownRefresh: {
          threshold: 90,
          stop: 50,
          txt: '刷新成功'
        },
        pullUpLoad: {
          threshold: 0,
          txt: {
            more: '加载更多',
            noMore: '没有更多的比赛啦'
          }
        },
        stopPropagation: true
      }
    }
  },
  watch: {
    source () {
      this.matchList = getMatchList(this.source, this.type)
    }
  },
  created () {
    this.subscribeDialog = this.$createSubscribeDialog()
  },
  methods: {
    clickItem (item) {
      console.log(`click: ${item.hostTeamName} vs ${item.guestTeamName}`)
    },
    subscribe () {
      this.subscribeDialog.show()
    },
    onPullingDown () {
      this.loadMatch('down')
    },
    onPullingUp () {
      this.loadMatch('up')
    },
    loadMatch (type) {
      setTimeout(() => {
        if (Math.random() > 0.5) {
          let match = []
          for (let index = 5; index > 0; index--) {
            match.push(this.matchList[index])
          }
          if (type === DOWN) {
            this.matchList.unshift(...match)
          } else if (type === UP) {
            this.matchList = this.matchList.concat(match)
          }
        } else {
          this.$refs.scroll.forceUpdate()
          if (type === UP) {
            setTimeout(() => {
              this.$refs.scroll.scroll.scrollBy(0, 64, 800)
            }, 1000)
          }
        }
      }, 1000)
    }
  }
}
</script>

<style lang="stylus">
.match-list
  height: 100%
  background-color: #E2E5EA
  .match-inner
    background-color: #FFFFFF
    .match-item
      border-bottom: 1px solid #E4E4E4
      padding: 10px 0
      display: flex
      justify-content: space-around
      .left-team,.right-team
        text-align: center
        width: 80px
        img
          display: inline-block
          height: 38px
          margin-bottom: 7px
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
          margin-bottom: 7px
        .order
          display: inline-block
          border:1px #007100 solid
          color: #49873D
          border-radius: 25px
          line-height: 16px
          padding: 3px 20px
          margin-bottom: 7px
        .end
          background-color: #E86F5D
        .score
          font-size: 14px
          font-weight: 500
          margin-bottom: 7px
          position: relative
          .order
            display: inline-block
            border-radius: 25px
            border:1px #2F6220 solid
            padding: 3px 20px
            font-size: 100%
            position: absolute
            right: -100px
            transform: translateY(-50%)
        .last
          font-size: 22px
          margin-top: 5px
          color: #878F98
        .time
          color: #92929A
.before-trigger, .cube-pulldown-wrapper
  color: #7D7D7D
  font-size: 12px
  line-height: 20px
</style>
