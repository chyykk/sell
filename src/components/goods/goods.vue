<template>
  <div class="goods">
    <div class="left-list" ref="menuWrapper">
        <ul>
          <li class="list" v-for="good,key in goods" :class="{'current':currentIndex===key}" @click = "selectMenu(key, $event)">
            <span class="text">
              <span class=""></span>
              {{good.name}}
            </span>
          </li>
        </ul>
    </div>
    <div class="food-wrapper" ref="foodsWrapper">
      <ul>
        <li class="food-list food-list-hook" v-for = "item in goods">
          <h1>{{item.name}}</h1>
          <ul>
            <li v-for = "item in item.foods" class="food-item border-1px">
              <div class="food-icon">
                <img :src="item.icon" alt=""/>
              </div>
              <div class="food-content">
                <div class="name">{{item.name}}</div>
                <div class="desc">{{item.description}}</div>
                <div class="extra">
                  <span class="count">月售{{item.sellCount}}份</span>
                  <span>好评率{{item.rating}}%</span>
                </div>
                <div class="price">
                  <span class="now">￥{{item.price}}</span>
                  <span class="old" v-show="item.oldPrice">￥{{item.oldPrice}}</span>
                </div>
                <div class="cartcontrol">qqq</div>
              </div>
            </li>
          </ul>
        </li>
      </ul>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  import BScroll from 'better-scroll';
  const ERR_OK = 0;
export default {
  data() {
    return {
      goods: [],
      listHeight: [],
      scrollY: 0
    };
  },
  created() {
  this.$http.get('/api/goods').then((response) => {
    response = response.body;
    if (response.err === ERR_OK) {
      this.goods = response.data;
      this.$nextTick(() => {
        this._initScroll();
        this._calculateHeight();
        console.log(this.listHeight);
      });
    };
  });
},
  computed: {
    currentIndex() {
      for (let i = 0; i < this.listHeight.length; i++) {
        let height1 = this.listHeight[i];
        let height2 = this.listHeight[i + 1];
        if (!height2 || (this.scrollY >= height1 && this.scrollY < height2)) {
          return i;
        }
      }
      return 0;
    }
  },
  methods: {
    selectMenu(index, event) {
      if (!event._constructed) {
        return;
      }
      console.log(index);
      let foodList = this.$refs.foodsWrapper.getElementsByClassName('food-list-hook');
      let el = foodList[index];
      this.foodsScroll.scrollToElement(el, 300);
    },
    _initScroll() {
      this.meunScroll = new BScroll(this.$refs.menuWrapper, {
        click: true
      });

      this.foodsScroll = new BScroll(this.$refs.foodsWrapper, {
        click: true,
        probeType: 3
      });

      this.foodsScroll.on('scroll', (pos) => {
        this.scrollY = Math.abs(Math.round(pos.y));
      });
    },
    _calculateHeight() {
      let foodList = this.$refs.foodsWrapper.getElementsByClassName('food-list-hook');
      let height = 0;
      this.listHeight.push(height);
      for (let i = 0; i < foodList.length; i++) {
        let item = foodList[i];
        height += item.clientHeight;
        this.listHeight.push(height);
      }
    }
  }
};
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "../../common/stylus/index.styl";
.goods
  position:absolute
  top:174px
  bottom:46px;
  overflow:hidden
  width:100%
  .left-list
      width:80px
      height:100%
      float:left
      background: #f3f5f7
      .list
        width:56px
        height:54px
        padding: 0 12px
        display:table
        &.current
          position:relative
          z-index:10
          margin-top:-1px
          background:#ffffff
          .text
            border-none()
        .text
          width:56px
          display:table-cell
          vertical-align:middle
          border-1px(rgba(7, 17, 27, 0.1))
          font-size:12px
  .food-wrapper
      margin-left:82px
      height:100%
      box-sizing:border-box
      .food-list
        h1
          height:26px
          background:#f3f5f7
          border-left:2px solid #d9dde1
          line-height:26px
          padding-left:14px
          font-size:12px
          color:rgb(147,153,159)
        .food-item
          display:flex
          margin:16px
          padding-bottom:18px
          border-1px(rgba(7,17,27,0.1))
        &:last-child
          border-none()
          margin-bottom:0
        .food-icon
          flex:0 0 57px
          margin-right:10px
          img
            width:57px
            height:57px
       .food-content
        padding-top:2px
        .name
          font-size:14px
          color:rgb(7,17,27)
          line-height:14px
        .desc
          font-size:10px
          color:rgb(147,153,159)
          margin:8px 0
        .extra
          font-size:10px
          margin-bottom:8px
          color:rgb(147,153,159)
          .count
            margin-right:12px
        .price
          line-height:14px
          font-weight:700
          .now
            margin-right:8px
            font-size:14px
            color:rgb(240,20,20)
          .old
            text-decoration:line-through
            font-size:10px
            color:rgb(147,153,159)
        .cartcontrol
          position:absolute
          right:0
          bottom:12px





</style>
