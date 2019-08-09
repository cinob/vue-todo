<template>
  <section class="real-app">
    <input
      type="text"
      class="add-input"
      autofocus="autofocus"
      placeholder="接下来要去做什么？"
      @keyup.enter="addTodo"
    >
    <item
      :todo="todo"
      v-for="todo in filteredTodos"
      :key="todo.id"
      @del="delTodo"
      @toggle="toggle"
    >
    </item>
    <tabs
      :filter="filter"
      :todos="todos"
      @toggle="toggleFilter"
      @clearAllCompleted="clearAllCompleted"
    ></tabs>
  </section>
</template>

<script>
import Item from './Item'
import Tabs from './Tabs'
export default {
  data () {
    return {
      todos: [],
      filter: 'all'
    }
  },
  components: {
    Item,
    Tabs
  },
  computed: {
    filteredTodos () {
      if (this.filter === 'all') {
        return this.todos
      }
      const completed = this.filter === 'completed'
      return this.todos.filter(todo => completed === todo.completed)
    }
  },
  methods: {
    addTodo (e) {
      this.todos.unshift({
        id: this.todos.length +1,
        content: e.target.value.trim(),
        completed: false
      })
      e.target.value = ''
    },
    delTodo (id) {
      this.todos.splice(this.todos.findIndex(todo => todo.id === id), 1)
    },
    toggleFilter (state) {
      this.filter = state
    },
    clearAllCompleted () {
      this.todos = this.todos.filter(todo => !todo.completed)
    },
    getTodos () {
      let t = localStorage.getItem('todos')
      if (t)
        this.todos = JSON.parse(t)
    },
    toggle (id) {
      let index = this.todos.findIndex(todo => todo.id === id)
      this.todos[index].completed = !this.todos[index].completed
      this.updateTodos()
    },
    updateTodos () {
      let t = JSON.stringify(this.todos)
      localStorage.setItem('todos', t)
    }
  },
  updated () {
    this.updateTodos()
  },
  mounted () {
    this.getTodos()
  }

}
</script>

<style lang="stylus" scoped>
@import "../assets/styles/global.styl"
.real-app
  width: px2rem(600)
  margin: 0 auto
  box-shadow: 0 0 px2rem(5) #666
  box-sizing: border-box
.add-input
  position: relative
  margin: 0
  width: 100%
  font-size: px2rem(24)
  font-family: inherit
  font-weight: inherit
  line-height: 1.4em
  border: 0
  outline: none
  color: inherit
  padding: px2rem(6)
  border: px2rem(1) solid #999
  box-shadow: inset 0 -px2rem(1) px2rem(5) 0 rgba(0,0,0,.06)
  box-sizing: border-box
  font-smoothing: antialiased
  padding: px2rem(16) px2rem(16) px2rem(16) px2rem(60)
  border: none;
  box-shadow: inset 0 -px2rem(2) px2rem(1) rgba(0,0,0,.06)
</style>
