<template>
  <div>
    <v-header :seller="seller"></v-header>
    <div class="tab border-1px">
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
import vHeader from './components/header/header';

const ERR_OK = 0;

export default {
  components: {
    vHeader
  },
  data () {
    return {
      seller: {}
    };
  },
  created () {
    this.$http.get('/api/sellers').then((response) => {
      response = response.body;
      if (response.errno === ERR_OK) {
        this.seller = Object.assign({}, this.seller, response.data);
      }
    });
  }
};
</script>

<style lang="stylus">
  @import 'common/stylus/index.styl';

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
        &.active
          color #f01414
</style>
