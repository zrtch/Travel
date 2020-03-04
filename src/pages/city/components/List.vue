<template>
  <div class="list" ref="wrapper">
    <div>
      <div class="area">
        <div class="title  border-topbottom">当前城市</div>
        <div class="button-list">
          <div class="button-wrapper">
            <div class="button">{{this.currentCity}}</div>
          </div>
        </div>
      </div>
      <div class="area">
        <div class="title  border-topbottom">热门城市</div>
        <div class="button-list">
          <div class="button-wrapper" v-for="item of hotCities" :key="item.id"
          @click="hanleCityClick(item.name)">
            <div class="button">{{item.name}}</div>
          </div>
        </div>
      </div>
      <div class="area" v-for="(item,key) of cities" :key="key" :ref="key">
        <div class="title border-topbottom">{{key}}</div>
        <div class="item-list">
          <div class="item border-bottom"
          v-for="innerItem of item"
          :key="innerItem.id"
           @click="hanleCityClick(innerItem.name)"
          >{{innerItem.name}}</div>

        </div>
      </div>
    </div>
  </div>
</template>

<script>
import {mapState, mapMutations} from 'vuex'
import Bscroll from 'better-scroll'
export default {
  name: 'CityList',
  props: {
    hotCities: Array,
    cities: Object,
    letter: String
  },
  computed: {
    ...mapState({
      currentCity: 'city'
    })
  },
  methods: {
    hanleCityClick(city) {
      this.changeCity(city)
      this.$router.push('/')
    },
    ...mapMutations(['changeCity'])
  },
  watch: {
    letter() {
      if (this.letter) {
        const element = this.$refs[this.letter][0]
        this.scroll.scrollToElement(element)
      }
    }
  },
  mounted() {
    this.scroll = new Bscroll(this.$refs.wrapper)
  }
}
</script>

<style lang="stylus" scoped>
@import '../../../assets/styles/varibles'
.border-topbottom
    &:before
        border-color:#ccc
    &:after
        border-color :#ccc
.border-bottom
    &:before
        border-color:#ccc
.list
    overflow :hidden
    position: absolute
    top:1.64rem
    left:0
    right:0
    bottom:0
    .title
        line-height :.48rem
        fons-size:.26rem
        background :#eee
        padding-left:.2rem
        color:#666
    .button-list
        overflow :hidden
        padding:.1rem .6rem .1rem .1rem
        .button-wrapper
            width:33.33%
            float:left
            .button
                text-align:center
                padding:.1rem 0
                margin:.1rem
                border:.02rem solid #ccc
                border-radius :.06rem
    .item-list
        .item
            line-height:.76rem
            padding-left:.2rem
</style>
