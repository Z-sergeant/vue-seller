<template>
  <div>
       <v-header :seller="seller"></v-header>
       <div class="tab">
          <router-link to="/goods" class="tab-item">商品</router-link>
          <router-link to="/ratings" class="tab-item">评论</router-link>
          <router-link to="/seller" class="tab-item">商家</router-link>
       </div>
       <router-view :seller="seller"></router-view>
  </div>
</template>

<script type="text/ecmascript-6">
   import header from './components/header/header.vue';
   const ERR_OK = 0;
   export default{
      data () {
        return {
          seller: {}
        };
      },
      created () {
         this.$http.get('/api/seller').then((response) => {
             response = response.body;
             console.log(response);
             if (response.errno === ERR_OK) {
                this.seller = response.data;
                console.log(this.seller.avatar);
             };
         });
         console.log(ERR_OK);
      },
      components: {
         'v-header': header
      }
   };
</script>

<style lang="stylus" rel ="stylesheet/stylus">
       .tab
           display:flex
           width:100%
           height:40px
           line-height:40px
           border-bottom: 1px solid #000
           .tab-item
                flex:1
                text-align:center
                text-decoration:none
                font-size:14px
                display:inline-block
       .router-link-active
           color:#fff
           background-color:red
</style>
