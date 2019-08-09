<template>
  <div id="app">
    <div id="cover"></div>
    <Header></Header>
    <Todo></Todo>
    <Footer></Footer>
  </div>
</template>

<script>
import Header from '../components/Header'
import Todo from '../components/Todo'
import Footer from '../components/Footer'

export default {
  components: {
    Header,
    Todo,
    Footer
  }
}
</script>

<style lang="stylus" scoped>
#app
  position: absolute
  left: 0
  right: 0
  top: 0
  bottom: 0
  #cover
    position: absolute
    left: 0
    top: 0
    right: 0
    bottom: 0
    background-color: #999
    opacity: .9
    z-index: -1
</style>
