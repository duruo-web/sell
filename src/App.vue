<template>
  <div id="app">
    <div class="header">
      <v-header :seller="seller"></v-header>
    </div>
    <div class="tab border-1px">
      <div class="tab-item">
        <router-link :to="{path: '/goods'}" tag="a">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link :to="{path: '/ratings'}" tag="a">评论</router-link>
      </div>
      <div class="tab-item">
        <router-link :to="{path: '/seller'}" tag="a">商家</router-link>
      </div>
    </div>
    <router-view :seller="seller"></router-view>
  </div>
</template>

<script type="text/ecmascript-6">
  import header from './components/header/header.vue'

  const ERR_OK = 0
  export default {
    data () {
      return {
        seller: {}
      }
    },
    created () {
      this.$http.get('/api/seller').then((response) => {
        response = response.body
        if (response.errno === ERR_OK) {
          this.seller = response.data
          console.log(this.seller)
        }
      })
    },
    components: { 'v-header': header }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "./common/stylus/mixin.styl"
  #app
    .tab
      display: flex
      width: 100%
      height: 40px
      line-height: 40px
      border-1px(rgba(7,17,27,.1))
      .tab-item
        flex: 1px
        text-align: center
        & > a
          display: block
          font: 14px
          coloe: rgb(77, 85, 93)
          &.active
            color: rgb(240,20,20)
</style>
