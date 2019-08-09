<template>
  <div id="footer">
    <span>Writen by {{this.author}}</span>
  </div>
</template>

<script>
export default {
  data () {
    return {
      author: 'Cinob'
    }
  }
}
</script>

<style lang="stylus" scoped>
@import "../assets/styles/global.styl"
#footer
  margin-top: px2rem(40)
  text-align: center
  color: #bfbfbf
  font-size: px2rem(10)
  text-shadow: 0 1px 0 #bfbfbf
</style>
