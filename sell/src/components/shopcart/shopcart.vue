<template>
  <div class="shopcart">
       <div class="content">
            <div class="content-left">
                <div class="logo-wrapper">
                    <div class="logo" :class="{'highlight':totalCount>0}">

                    </div>
                    <div class="num" v-show="totalCount>0">{{totalCount}}</div>
                </div>
                <div class="price">
￥{{totalPrice}}
                </div>
                <div class="desc">
另需配送费￥{{deliveryPrice}}
                </div>
            </div>
            <div class="content-right">
                 <div class="pay" :class="payClass">
                     {{payDesc}}
                 </div>
            </div>
       </div>
  </div>
</template>

<script type="text/ecmascript-6">
   export default{
      props: {
         selectFoods: {
            type: Array,
            default () {
               return [
                  {
                     price: 50,
                     count: 2
                  }
               ];
            }
         },
         deliveryPrice: {
            type: Number,
            default: 0
         },
         minPrice: {
            type: Number,
            default: 0
         }
      },
      computed: {
         totalPrice () {
             let total = 0;
             this.selectFoods.forEach((food) => {
                 total += food.price * food.count;
             });
             return total;
         },
         totalCount () {
             let count = 0;
             this.selectFoods.forEach((food) => {
                 count += food.count;
             });
             return count;
         },
         payDesc () {
             if (this.totalPrice === 0) {
                return `￥${this.minPrice}元起送`;
             } else if (this.totalPrice < this.minPrice) {
                let diff = this.minPrice - this.totalPrice;
                return `还差￥${diff}元起送`;
             } else {
                return `去结算`;
             }
         },
         payClass () {
             if (this.totalPrice < this.minPrice) {
                 return `not-enough`;
             } else {
                 return `enough`;
             }
         }
      }
   };
</script>

<style lang="stylus" rel="stylesheet/stylus">
   .shopcart
      position: fixed
      bottom: 0
      left: 0
      z-index: 50
      width: 100%
      height: 48px
      background-color: #f1f1f1
      .content
          display: flex
          background: #141d27
          font-left: 0
          .content-left
             flex: 1
             .logo-wrapper
                display: inline-block
                position: relative
                top: -10px
                margin: 0 12px
                padding: 6px
                width: 56px
                height: 56px
                box-sizing: border-box
                background-color: #00bfff
                border-radius: 50%
                vertical-align: top
                .logo
                   width: 100%
                   height: 100%
                   border-radius: 50%
                   background-color: #2b343c
                   $.highlight
                      background-color: rgb(0,160,220)
                .num
                   position: absolute
                   top: 0
                   right: 0
                   width: 24px
                   height: 16px
                   line-height: 16px
                   text-align: center
                   border-radius: 16px
                   font-size: 9px
                   font-weight: 700
                   color: #fff
                   background: rgb(240,20,20)
                   box-shadow: 0 4px 8px 0 rgba(0,0,0,0.4)
             .price
                display: inline-block
                vertical-align: top
                line-height: 24px
                margin-top: 12px
                margin-right: 12px
                box-sizing: border-box
                font-weight: 700
                color: #f5f5f5
                font-size: 16px
             .desc
                display: inline-block
                vertical-align: top
                line-height: 24px
                margin: 12px 0 0 6px
                font-size: 10px
                color: #fff
          .content-right
             flex: 0 0 104px
             width: 105px
             .pay
               height: 48px
               line-height: 48px
               text-align: center
               font-size: 14px
               font-weight: 700
               color: #fff
               &.not-enough
                  background: #2b333b
               $.enough
                  background: #00b43c
                  color: #fff
</style>
