<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
    <div class="tab">
      <div class="tab-item">
        <router-link to="/goods">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/ratings">评论</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/sellers">商家</router-link>
      </div>
    </div>
    <router-view></router-view>
  </div>
</template>

<script>
  import header from './components/header/Header';

  const ERR_OK = 0;

  export default {
    data () {
      return {
        seller: this.seller
      };
    },
    created () {
      this.$http.get('/api/seller').then(async (response) => {
        const res = await response.json();
        if (res.errno === ERR_OK) {
          this.seller = res.data;
        }
      });
    },
    components: {
      'v-header': header
    },
    name: 'App'
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "./common/stylus/mixin"

  #app
    .tab
      display flex
      width 100%
      height 40px
      line-height 40px
      border-1px(rgba(7, 17, 27, 0.1))
      .tab-item
        flex 1
        text-align center
        & > a
          display block
          font-size 14px
          color rgb(77, 85, 93)
          &.router-link-active
            color rgb(240, 20, 20)
</style>
