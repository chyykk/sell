<template>
  <div class="header">
      <div class="content-wrap">
          <div class="avatar">
              <img width="64" height="64" alt="" :src="seller.avatar"/>
          </div>
          <div class="content">
              <div class="title">
                  <span class="brand"></span>
                  <span class="name">{{seller.name}}</span>
              </div>
              <div class="description">
                  {{seller.description}}/{{seller.deliveryTime}}分钟送达
              </div>
              <div v-if="seller.supports" class="supports">
                  <span class="icon" :class="classMap[seller.supports[0].type]"></span>
                  <span class="text">{{seller.supports[0].description}}</span>
              </div>
          </div>
          <div class="support-content" @click="showDetail">
             <span class="count">{{seller.supports.length}}个</span>
              <span class="icon-keyboard_arrow_right"></span>
          </div>
      </div>
      <div class="bulletin-wrap">
            <span class="bulletin-title"></span><span class="bulletin-text">{{seller.bulletin}}</span>
            <span class="icon-keyboard_arrow_right"></span>
      </div>
      <div class="background">
        <img :src="seller.avatar" width="100%" height="100%" alt=""/>
      </div>
      <div class="detail" v-show="detailShow">
         <div class="detail-wrapper clearfix">
           <div class="detail-main">
             <h1 class="name">{{seller.name}}</h1>
             <span class="seller-star"></span>
             <div class="title-wrap"><span class="hr"></span><span class="title">优惠信息</span><span class="hr"></span></div>
             <div class="supports-text">
               <div v-for="v in seller.supports"><span class="icon" :class="classMap[v.type]"></span><span class="text">{{v.description}}</span></div>
             </div>
             <div  class="title-wrap"><span class="hr"></span><span  class="title">商家公告 </span><span class="hr"></span></div>
             <div class="bulletin-text">{{seller.bulletin}}</div>
           </div>
         </div>
         <div class="detail-close">
           <i class="icon-close" @click="hideDetail"></i>
         </div>
      </div>
  </div>
</template>

<script type="text/ecmascript-6">
export default {
    props: {
        seller: {
            type: Object
        }
    },
    data() {
       return {
         detailShow: false
       };
    },
    methods: {
      showDetail() {
        this.detailShow = true;
      },
      hideDetail() {
        this.detailShow = false;
      }
    },
    created() {
        this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee'];
    }
};
</script>

<style lang="stylus" rel="stylesheet/stylus">
    @import "../../common/stylus/index.styl";
    @import "../../common/stylus/icon.css";
    .header
      position:relative
      overflow:hidden
      color:#fff
      background:rgba(7,17,27,0.5)
      .content-wrap
         padding:24px 12px  18px 24px
         font-size:0
         position:relative
         .avatar
            display:inline-block
            margin-right:16px
            vertical-align:top
         .content
            display:inline-block
            .title
              margin:2px 0  8px 0
              font-weight:bold
              font-size:16px
              line-height:18px
              .brand
                 vertical-align:bottom
                 display:inline-block
                 width:30px
                 height:18px
                 bg-img('brand')
                 background-size: 30px 18px
                 background-position:no-repeat
            .description
               margin-bottom:10px
               font-weight:200
               font-size:12px
            .supports
               font-weight:200
               font-size:10px
               .icon
                 vertical-align:middle
                 display:inline-block
                 margin:0 4px 2px 0
                 width:12px
                 height:12px
                 background-size: 12px 12px
                 background-position:no-repeat
                 &.decrease
                   bg-img('decrease_1')
                 &.discount
                   bg-img('discount_1')
                 &.guarantee
                   bg-img('guarantee_1')
                 &.special
                   bg-img('special_1')
                 &.invoice
                   bg-img('invoice_1')
         .support-content
            position:absolute
            right:14px
            bottom:18px
            padding :0px 8px
            height:24px
            font-size:10px
            border-radius:14px
            background:rgba(0,0,0,0.2)
            .count
              display:inline-block
              text-algin:center
              line-height:24px
            .icon-keyboard_arrow_right
              display:inline-block
              font-size:10px
              line-height:24px
    .bulletin-wrap
      position:relative
      background:rgba(7,17,27,0.2)
      height:28px
      line-height:28px
      padding:0 22px 0 12px
      white-space:nowrap
      text-overflow:ellipsis
      overflow:hidden
      .bulletin-title
        display:inline-block
        vertical-align:middle
        font-size:10px
        width:22px
        height:12px
        bg-img('bulletin')
        background-size:22px 12px
        background-position:no-repeat
      .bulletin-text
        vertical-align:middle
        font-size:10px
        margin-left:4px
      .icon-keyboard_arrow_right
        position:absolute
        font-size:10px
        right:10px
        top:8px
    .background
       position:absolute
       top:0
       left:0
       width:100%
       height:100%
       z-index:-1
       filter:blur(10px)
    .detail
       position:fixed
       left:0
       top:0
       z-index:100
       width:100%
       height:100%
       overflow:auto
       background:rgba(7,17,27,0.8)
       .detail-wrapper
         min-height:100%
         .detail-main
           margin-top:64px
           padding-bottom:64px
           .name
             text-align:center
             font-size:16px
             line-height:16px
             font-weight:700
             marign-bottom:16px
           .title-wrap
              text-align:center
              margin:28px 0 24px 0
           .hr
             display:inline-block
             width:112px
             border-top:2px solid rgba(255,255,255,0.2)
             text-align:center
             vertical-align:middle
           .title
              display:inline-block
              margin:0 12px
              font-size:14px
              font-weight:700
              line-height:14px
           .supports-text
              margin:0 36px
              .icon
                display:inline-block
                width:16px
                height:16px;
           .bulletin-text
              margin:0 36px
              font-size:12px
              color:rgb(255,255,255)
              line-height:2
              padding:0 12px
              text-align:justify
       .detail-close
         position:relative
         width:32px
         height:32px
         font-size:32px
         margin:-64px auto 0 auto



</style>
