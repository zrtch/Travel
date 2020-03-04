<template>
  <div class="header">
    <div class="header-left">
      <div class="iconfont back-icon">&#xe624;</div>
    </div>
    <div class="header-input">
      <span class="iconfont">&#xe632;</span>
      输入城市经典游玩主题
    </div>
    <div class="header-right">
      {{this.city}}
      <span class="iconfont arrow-icon">&#xe62a;</span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HomeHeader',
  props: {
    city: String
  }
}
</script>

<style lang="stylus" scoped>
@import '../../../assets/styles/varibles'
    .header
        display:flex
        line-height:.86rem
        background:$bgColor
        color:white
        .header-left
            widht:.64rem
            float:left
            .back-icon
                text-align:center
                font-size:.4rem
        .header-input
            flex:1
            height:.66rem
            background:#fff
            line-height:.66rem
            border-radius:.1rem
            margin-left:.2rem
            margin-top:.10rem
            padding-left:.2rem
            color:#ccc
        .header-right
            width:1.24rem
            float:right
            text-align:center
            .arrow-icon
                font-size:.24rem
</style>
