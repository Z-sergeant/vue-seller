<template>
  <div class="cartcontrol">
      <div class="cart-decrease" v-show="food.count>0" @click="decreaseCart">-</div>
      <div class="cart-count" v-show="food.count>0">{{food.count}}</div>
      <div class="cart-add" @click="addCart">+</div>
  </div>
</template>

<script type="text/ecmascript-6">
   import Vue from 'vue';

   export default{
      props: {
         food: {
            type: Object
         }
      },
      created () {
      },
      methods: {
         addCart (event) {
            if (!event._constructed) {
              return;
            }
            if (!this.food.count) {
               Vue.set(this.food, 'count', 1);
            } else {
               this.food.count ++;
            }
            console.log(this.food.count);
         },
         decreaseCart (event) {
            if (!event._constructed) {
              return;
            }
            if (this.food.count) {
               this.food.count --;
            }
         }
      }
   };
</script>

<style lang="stylus" rel="stylesheet/stylus">
   .cartcontrol
       font-size: 0
       .cart-decrease
          display: inline-block
          padding: 6px
          font-size: 24px
          line-height: 24px
          height: 24px
          width: 24px
          text-align: center
          color: #fff
          background: rgb(0,160,220)
          border-radius: 50%
       .cart-count
          display: inline-block
          vertical-align: top
          width: 12px
          padding: 6px 12px 0 12px
          line-height: 24px
          text-align: center
          font-size: 10px
          color: rgb(147,153,159)
       .cart-add
          float: right
          display: inline-block
          padding: 6px
          font-size: 24px
          line-height: 24px
          height: 24px
          width: 24px
          text-align: center
          color: #fff
          background: rgb(0,160,220)
          border-radius: 50%
</style>
