<template>
<div>
  <div class="search">
    <input v-model="keyword" class="search-input" type="text" placeholder="输入城市名或拼音">
  </div>
    <div class="search-content" ref="search" v-show="keyword">
      <ul>
        <li class="search-item border-bottom" v-for="item of list" :key="item.id">{{item.name}}</li>
        <li class="search-item border-bottom" v-show="hasNoData">没有找到匹配数据</li>
      </ul>
    </div>
</div>

</template>

<script>
import Bscroll from 'better-scroll'
export default {
  name: 'CitySearch',
  props: {
    cities: Object
  },
  computed: {
    hasNoData() {
      return !this.list.length
    }
  },
  data() {
    return {
      keyword: '',
      list: [],
      timer: null
    }
  },
  watch: {
    keyword() {
      if (this.timer) {
        clearTimeout(this.timer)
      }
      if (!this.keyword) {
        this.list = []
        return
      }
      this.timer = setTimeout(() => {
        const result = []
        for (let i in this.cities) {
          this.cities[i].forEach((value) => {
            if (value.spell.indexOf(this.keyword) > -1 || value.name.indexOf(this.keyword) > -1) {
              result.push(value)
            }
          })
        }
        this.list = result
      }, 100)
    }
  },
  mounted() {
    this.scroll = new Bscroll(this.$refs.search)
  }
}
</script>

<style lang="stylus" scoped>
@import '../../../assets/styles/varibles'
.search
    height :.72rem
    background :$bgColor
    padding:0 .1rem
    .search-input
        width:100%
        height :.62rem
        line-height:.62rem
        text-align :center
        color:#666
        box-sizing :border-box
        padding:0 .1rem
.search-content
  position :absolute
  overflow :hidden
  z-index:1
  top:1.58rem
  right:0
  left:0
  bottom:0
  background #ee
  .search-item
    line-height .62rem
    padding .2rem
    background #fff
    color #666
</style>
