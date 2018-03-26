<template>
  <div id="app">
    <div class="header">
      <h1 class="title" @click="showPicker">
        <span>{{source}}赛事</span>
        <i class="cubeic-select" :class="{down: toDown}"></i>
      </h1>
      <div class="navigator">
        <ul class="nav-list">
          <li v-for="(item, index) in tabList" :key="index"
            @click="switchTab(index)" :class="{active: currentPage === index}">
            {{ item.txt }}
          </li>
        </ul>
        <i class="triangle-up" :class="{left: currentPage === 0, right: currentPage === 2}"></i>
      </div>
    </div>
    <div class="content">
      <cube-slide
        :data="tabList"
        :initialIndex="currentPage"
        :loop="false"
        :autoPlay="false"
        :threshold="0.1"
        @change="slideChange">
        <cube-slide-item v-for="(item, index) in tabList" :key="index">
          <div class="match-list-wrapper">
            <match-list :source="source" :type="item.type"></match-list>
          </div>
        </cube-slide-item>
        <div slot="dots"></div>
      </cube-slide>
    </div>
  </div>
</template>

<script>
import { ENDED, LIVE, CONCERN } from './common/config/tabs'
import MatchList from './components/match-list'

export default {
  name: 'app',
  data () {
    return {
      currentPage: 1,
      tabList: [
        {
          txt: '已结束',
          type: ENDED
        },
        {
          txt: '我的关注',
          type: CONCERN
        },
        {
          txt: '直播中',
          type: LIVE
        }
      ],
      toDown: false,
      pickerList: [
        {text: 'NBA', value: 'NBA'},
        {text: 'DOTA', value: 'dota'},
        {text: 'SOCCER', value: 'soccer'}
      ],
      source: 'soccer'
    }
  },
  mounted () {
    this.picker = this.$createPicker({
      title: '赛事',
      data: [this.pickerList],
      selectedIndex: [2],
      onSelect: () => {
        this.toDown = false
      },
      onCancel: () => {
        this.toDown = false
      },
      onValueChange: (selectedVal) => {
        this.source = selectedVal[0]
      }
    })
  },
  methods: {
    switchTab (index) {
      this.currentPage = index
    },
    slideChange (index) {
      this.currentPage = index
    },
    showPicker () {
      this.toDown = true
      this.picker.show()
    }
  },
  components: {
    MatchList
  }
}
</script>

<style lang="stylus">
@import './common/stylus/mixin.styl'
html, body, #app
  height: 100%
  text-align: center
#app
  background-color: color_grey
  .header
    color: white
    background-color: #15191D
    .title
      padding: 20px 0
      font-size: 16px
      color: white
      display: inline-block
      .down
        display: inline-block
        transform: rotate(180deg)
    .navigator
      position: relative
      padding-bottom: 12px
      font-size: 12px
      .nav-list
        display: flex
        justify-content: space-around
        li
          width: 60px
          color: #E0E4E8
          &.active
            color: white
    .triangle-up
      position: absolute
      left: 50%
      transform: translate(-50%, 0)
      bottom: 0
      width: 0
      height: 0
      border-left: 7px solid transparent
      border-right: 7px solid transparent
      border-bottom: 8px solid color_grey
      transition: all 0.4s
      &.left
        left: 16.67%
      &.right
        left: 83.34%
  .content
    height: calc(100% - 80px)
    overflow: hidden
    .match-list-wrapper
      height: 100%
      background-color: #E2E5EA
</style>
