<template>
 <div class="cartcontrol">
   <div class="cart-decrease"></div>
   <div class="cart-count"></div>
   <div class="cart-add"></div>
 </div>
</template>

<script type="text/ecmascript-6">
export default {}
</script>

<style lang="stylus" rel="stylesheet/stylus">
.cartcontrol
  font-size:0
  .cart-decrease
    display:inline-block
    padding:6px
    transtion:all 0.4s linear
    &.move-transition
      opacity:1
      transform:translate3d(0,0,0)

</style>
