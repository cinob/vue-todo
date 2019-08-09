<template>
  <div class="helper">
    <span class="left">{{unFinishedTodoLength}} items left</span>
    <span class="tabs">
      <span
        v-for="state in states"
        :key="state"
        :class="[state, filter === state ? 'actived' : '' ]"
        @click="toggleFilter(state)"
      >
        {{state}}
      </span>
    </span>
    <span class="clear" @click="clearAllCompleted">Clear Completed</span>
  </div>
</template>

<script>
export default {
  props: {
    filter: {
      type: String,
      required: true
    },
    todos: {
      type: Array,
      required: true
    }
  },
  data () {
    return {
      states: ['all', 'active', 'completed']
    }
  },
  computed: {
    unFinishedTodoLength () {
      return this.todos.filter(todo => !todo.completed).length
    }
  },
  methods: {
    clearAllCompleted () {
      this.$emit('clearAllCompleted')
    },
    toggleFilter (state) {
      this.$emit('toggle', state)
    }
  }
}
</script>

<style lang="stylus" scoped>
@import "../assets/styles/global.styl"
.helper
  font-weight: 100
  display: flex
  justify-content: space-between
  padding: px2rem(5) 0
  line-height: px2rem(30)
  background-color: #fff
  font-size: px2rem(14)
  font-smoothing: antialiased
.left, .clear, .tabs
  padding: 0 px2rem(10)
  box-sizing: border-box
.left, .clear
  width: px2rem(150)
.left
  text-align: left
.clear
  text-align: right
  cursor: pointer
.tabs
  width: px2rem(200)
  display: flex
  justify-content: space-around
  *
    display: inline-block
    padding: 0 px2rem(10)
    cursor: pointer
    border: px2rem(1) solid rgba(175, 47, 47, 0)
    &.actived
      border-color: rgba(175, 47, 47, 0.4)
      border-radius: px2rem(5)
</style>
