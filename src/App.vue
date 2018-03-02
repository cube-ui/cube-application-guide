<template>
  <div id="app">
    <div class="header">NBA</div>
    <div class="navigator">
      <ul class="tab-list">
        <li v-for="(item, index) in tabList" :key="index"
          @click="switchTab(index)" :class="{'active': currentPage === index}">
          {{ item }}
        </li>
      </ul>
    </div>
    <div class="content">
      <cube-slide
        :data="tabList"
        :loop="false"
        :autoPlay="false"
        :threshold="0.1"
        @change="slideChange()"
        >
        <cube-slide-item v-for="(item, index) in tabList" :key="index">
          <div class="match-list-wrapper">
            <match-list></match-list>
          </div>
        </cube-slide-item>
        <div slot="dots"></div>
      </cube-slide>
    </div>
  </div>
</template>

<script>
import MatchList from './components/match-list'

export default {
  name: 'app',
  data () {
    return {
      currentPage: 1,
      tabList: ['已结束', '未结束', '我的关注']
    }
  },
  components: {
    MatchList
  },
  methods: {
    switchTab (index) {
      this.currentPage = index
      console.log(index)
    },
    slideChange (index) {
      console.log(index)
      this.currentPage = index
    }
  }
}
</script>

<style lang="stylus">
html, body, #app
  height: 100%
  text-align: center
#app 
  .header
    height: 44px
    line-height: 44px
    background-color: #ea3b32
    color: white
  .tab-list
    height: 40px
    line-height: 44px
    display: flex
    justify-content: space-around
    border-bottom: solid 1px #f0f0f1
  .content
    height: calc(100% - 85px)
    overflow: hidden
  .active
    color: orange
</style>
