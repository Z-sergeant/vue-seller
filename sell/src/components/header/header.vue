<template>
  <div class="header">
       <div class="content-wrapper">
           <div class="avatar">
              <img width="64" height="64" :src="seller.avatar" />
           </div>
           <div class="content">
              <div class="title">
                  <span class="brand"></span>
                  <span class="name">{{seller.name}}</span>
              </div>
              <div class="description">
                   {{seller.description}}/{{seller.deliveryTime}}分钟
              </div>
              <div v-if="seller.supports" class="support" >
                    <span class="icon" :class="classMap[seller.supports[0].type]"></span>
                    <span class="text">{{seller.supports[0].description}}</span>
              </div>
           </div>
           <div v-if="seller.supports" class="support-count" @click="showDetail">
             <span class="count">{{seller.supports.length}}个</span>
           </div>
       </div>
       <div class="bulletin-wrapper">
           <span class="bulletin-title"></span>
           <span class="bulletin-text">{{seller.bulletin}}</span>
       </div>
       <div class="background">
            <img :src="seller.avatar" width="100%" height="100%" >
       </div>
       <transition name="fade">
           <div v-show="detailShow" class="detail">
                       <div class="detail-wrapper clearFix">
                             <div class="detail-main"></div>
                       </div>
                       <div class="detail-close" @click="closeDetail">
                         1111
                       </div>
           </div>
       </transition>

  </div>
</template>

<script type="text/ecmascript-6">
   export default{
      props: {
         seller: {
            type: Object
         }
      },
      data () {
         return {
           detailShow: false
         };
      },
      methods: {
        showDetail () {
          this.detailShow = true;
          console.log(this.detailShow);
        },
        closeDetail () {
          this.detailShow = false;
        }
      },
      created () {
         this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee'];
      }
   };
</script>

<style lang="stylus" rel ="stylesheet/stylus">
     .header
         color: #fff
         position: relative
         background: rgba(7,17,27,0.5)
         over-flow: hidden
         .content-wrapper
             position: relative
             padding: 24px 12px 18px 24px
             font-size: 0
             .avatar
                 display: inline-block
                 vertical-align: top
                 img
                    border-radius: 2px
             .content
                 display: inline-block
                 font-size: 14px
                 margin-left: 8px
                 .title
                    margin: 2px 0 8px 0
                    .brand
                       display: inline-block
                       vertical-align: top
                       width: 30px
                       height: 18px
                       background-image: url("brand@2x.png")
                       background-size:30px 18px
                       background-repeat: no-repeat
                    .name
                       margin-left: 6px
                       font-size: 16px
                       line-height: 18px
                       font-weight: bold
                 .description
                    margin-bottom: 10px
                    line-height: 12px
                    font-size: 12px
                 .support
                    .icon
                      display: inline-block
                      vertical-align: top
                      width: 12px
                      height: 12px
                      margin-right: 4px
                      background-size: 12px 12px
                      background-repeat: no-repeat
                      &.decrease
                         background-image: url("decrease_1@2x.png")
                      &.discount
                         background-image: url("discount_1@2x.png")
                      &.guarantee
                         background-image: url("guarantee_1@2x.png")
                      &.invoice
                         background-image: url("invoice_1@2x.png")
                    .text
                      line-height: 12px
                      font-size: 10px
             .support-count
                 position: absolute
                 right: 12px
                 bottom: 18px
                 padding: 0 8px
                 height: 24px
                 line-height: 24px
                 border-radius: 14px
                 background: rgba(0, 0, 0, 0.2)
                 text-align: center
                 .count
                   font-size: 12px
                   padding: 0 8px
         .bulletin-wrapper
             height: 28px
             line-height: 28px
             padding: 0 22px 0 12px
             font-size: 0
             background-color: rgba(7,17,24,0.2)
             white-span: nowrap
             overflow: hidden
             text-overflow: ellipsis
             .bulletin-title
                display: inline-block
                vertical-align: top
                margin-top: 8px
                width: 22px
                height: 22px
                background-image: url("bulletin@2x.png")
                background-size: 22px 12px
                background-repeat: no-repeat
             .bulletin-text
                display: inline-block
                vertical-align: top
                font-size: 10px
                width: 245px
                height: 22px
         .background
             position: absolute
             top: 0
             left: 0
             width: 100%
             height: 100%
             z-index: -1
             filter: blur(10px)
         .detail
             position: fixed
             z-index: 100
             top: 0
             left: 0
             width: 100%
             height: 100%
             overflow:auto
             transition: all 0.5s
             background: rgba(7,17,27,0.8)
             &.fade-enter-active
                 opacity: 0
                 background: rgba(7,17,27,0)
             &.fade-enter-to
                 opacity: 1
                 background: rgba(7,17,27,0.8)
             &.fade-leave-active
                 opacity: 1
                 background: rgba(7,17,27,0.8)
             &.fade-leave-to
                 opacity: 0
                 background: rgba(7,17,27,0)
             .detail-wrapper
                  min-height: 100%
                  .detail-main
                      padding-top: 64px
                      padding-bottom: 64px
             .detail-close
                   position: relative
                   bottom: -32px
                   width: 32px
                   height: 32px
                   margin: -64px auto 0 auto
                   clear: both
                   font-size: 12px
</style>
