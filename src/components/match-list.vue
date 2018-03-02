<template>
  <div class="match-list">
    <cube-scroll
      :data="matchList">
      <ul>
        <li v-for="(item, index) in matchList" :key="index">
          {{ item }}
        </li>
      </ul>
    </cube-scroll>
  </div>
</template>

<script>
export default {
  name: 'match-list',
  data () {
    return {
      matchList: ['比赛1', '比赛2']
    }
  }
}
</script>

<style>
.match-list {

}
</style>
