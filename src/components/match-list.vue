<template>
  <div class="match-list">
    <cube-scroll
      :data="matchList">
      <ul>
        <li v-for="(item, index) in matchList" :key="index" class="match-item">
          <div class="left-team">
            <img :src="item.hostLogoUrl" alt="" class="logo">
            <p class="name">{{item.hostTeamName}}</p>
          </div>
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
      matchList: [
        {
          'hostTeamName': '太阳',
          'hostLogoUrl': 'https://rl.aicai.com/images/pages/leaguelib/team_logo/tm_logo_84.png',
          'gustTeamName': '老鹰',
          'gustLogoUrl': 'https://rl.aicai.com/images/pages/leaguelib/team_logo/tm_logo_91.png',
          'hostScore': 2,
          'gestScore': 1,
          'endTime': '1小时24分钟后',
          'gust': true
        },
        {
          'hostTeamName': '步行者',
          'hostLogoUrl': 'https://rl.aicai.com/images/pages/leaguelib/team_logo/tm_logo_225.png',
          'gustTeamName': '奇才',
          'gustLogoUrl': 'https://rl.aicai.com/images/pages/leaguelib/team_logo/tm_logo_233.png',
          'hostScore': 2,
          'gestScore': 1,
          'endTime': '1小时24分钟后',
          'gust': true
        },
        {
          'hostTeamName': '骑士',
          'hostLogoUrl': 'https://rl.aicai.com/images/pages/leaguelib/team_logo/tm_logo_1935.png',
          'gustTeamName': '公牛',
          'gustLogoUrl': 'https://rl.aicai.com/images/pages/leaguelib/team_logo/tm_logo_456.png',
          'hostScore': 2,
          'gestScore': 1,
          'endTime': '1小时24分钟后',
          'gust': true
        },
        {
          'hostTeamName': 'Serect',
          'hostLogoUrl': 'https://rl.aicai.com/images/pages/leaguelib/team_logo/tm_logo_466.png',
          'gustTeamName': 'VGJ.T',
          'gustLogoUrl': 'https://rl.aicai.com/images/pages/leaguelib/team_logo/tm_logo_927.png',
          'hostScore': 2,
          'gestScore': 1,
          'endTime': '1小时24分钟后',
          'gust': true
        },
        {
          'hostTeamName': '凯尔特人',
          'hostLogoUrl': 'https://rl.aicai.com/images/pages/leaguelib/team_logo/tm_logo_7344.png',
          'gustTeamName': '灰熊',
          'gustLogoUrl': 'https://rl.aicai.com/images/pages/leaguelib/team_logo/tm_logo_2817.png',
          'hostScore': 2,
          'gestScore': 1,
          'endTime': '1小时24分钟后',
          'gust': true
        }
      ]
    }
  }
}
</script>

<style lang="stylus">
.match-list
  .match-item
    border-bottom: 1px solid #f0f0f1
    padding: 10px 0
    .left-team
      text-align: center
      img
        display: inline-block
        width: 35px
        height: 35px
        margin-bottom: 4px
      .name 
        font-size: 14px
</style>
