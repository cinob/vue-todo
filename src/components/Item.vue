<template>
  <div :class="['todo-item', todo.completed ? 'completed' : '']">
    <input
      type="checkbox"
      class="toggle"
      v-model="todo.completed"
      @click="toggle"
    >
    <label> {{todo.content}} </label>
    <button class="destory" @click="delTodo"></button>
  </div>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true
    }
  },
  methods: {
    delTodo () {
      this.$emit('del', this.todo.id)
    },
    toggle () {
      this.$emit('toggle', this.todo.id)
    }
  }
}
</script>

<style lang="stylus" scoped>
@import "../assets/styles/global.styl"
.todo-item
  position: relative
  background-color: #fff
  font-size: px2rem(24)
  border-bottom: px2rem(1) solid rgba(0,0,0,.06)
  &:hover
    .destory:after
      content: 'x'
  label
    white-space: pre-line
    word-break: break-all
    padding: px2rem(15) px2rem(60) px2rem(15) px2rem(15)
    margin-left: px2rem(45)
    display: block
    line-height: 1.2
    transition: color 0.4s
  &.completed
    label
      color: #d9d9d9
      text-decoration: line-through
.toggle
  text-align: center
  width: px2rem(40)
  height: px2rem(40)
  position: absolute
  top: 0
  bottom: 0
  margin: auto 0
  border: none
  appearance: none
  outline: none
  &:after
    content: url('../assets/images/round.svg')
    line-height: px2rem(63)
  &:checked:after
    content: url('../assets/images/done.svg')
.destory
  position: absolute
  top: 0
  right: px2rem(10)
  bottom: 0
  width: px2rem(40)
  height: px2rem(40)
  margin: auto 0
  font-size: px2rem(30)
  color: #cc9a9a
  margin-bottom: px2rem(11)
  transition: color 0.2s ease-out
  background-color: transparent
  appearance: none
  border-width: 0
  cursor: pointer
  outline: none
</style>
