<template>
  <div class="m-header">
    <div class="icon"></div>
    <router-link to="/user" class="mine" tag="div">
      <i class="icon-mine"></i>
    </router-link>
  </div>
</template>

<script type="text/ecmascript-6">
  export default {}
</script>

<style scoped lang="stylus" rel="stylesheet/stylus">
  @import "~common/stylus/variable"
  @import "~common/stylus/mixin"

  .m-header
    position: relative
    height: 44px
    text-align: center
    color: $color-theme
    .icon
      display: inline-block
      vertical-align: top
      margin-top: 6px
      width: 88px
      height: 32px
      margin-right: 9px
      bg-image('logo')
      background-size: 88px 32px
    .text
      display: inline-block
      vertical-align: top
      line-height: 44px
      font-size: 18px
    .mine
      position: absolute
      top: 0
      right: 0
      .icon-mine
        display: block
        padding: 12px
        font-size: 20px
        color: $color-theme
</style>
