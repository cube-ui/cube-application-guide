<template>
  <div class="match-list">
    <cube-scroll
      :data="matchList" :options="options">
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
          txt: 'Refresh success'
        }
      }
    }
  }
}
</script>

<style lang="stylus">
.match-list
  height: 618px
  .match-item
    border-bottom: 1px solid #f0f0f1
    padding: 10px 0
    display: flex
    .left-team,.right-team
      text-align: center
      flex: 1
      img
        display: inline-block
        width: 35px
        height: 35px
        margin-bottom: 4px
      .name 
        font-size: 14px
    .center
      flex-basis: 50%
      font-size: 12px
      .guest
        display: inline-block
        background-color: green
        color: white
        line-height: 16px
        padding: 3px 10px
        border-radius: 25px
        margin-bottom: 5px
      .end
        background-color: red
      .score
        font-size: 14px
        font-weight: 500
        margin-bottom: 5px
</style>
