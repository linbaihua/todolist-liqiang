<template>
  <div id="app">
    <div class="todo-container">
      <div class="todo-wrap">
        <TodoHeader :addTodo="addTodo" />
        <todo-list :todos="todos" :checkTodo="checkTodo" :deleteTodo="deleteTodo" />
        <TodoFooter />
      </div>
    </div>
  </div>
</template>

<script>
import TodoFooter from './components/TodoFooter.vue'
import TodoHeader from './components/TodoHeader.vue'
import TodoList from './components/TodoList.vue'

export default {
  name: 'App',
  components: { TodoFooter, TodoHeader, TodoList },
  data() {
    return {
      todos: [
        { id: '001', title: '抽烟', done: true },
        { id: '002', title: '喝酒', done: true },
        { id: '003', title: '开车', done: true }
      ]
    }
  },
  methods: {
    // 添加一个todo,传入一个todo对象
    addTodo(todo) {
      this.todos.unshirt(todo)
    },
    // 删除一个todo，传入一个todo对象
    deleteTodo(todo) {
      this.todos = this.todos.filter(todo => todo.id !== id)
    },
    // 勾选或者取消勾选一个todo，用 todo.id 判断
    checkTodo(id) {
      this.todos.forEach(todo => {
        if (todo.id === id) {
          todo.done = !todo.done
        }
      })
    },
    // 全选或者取消全选todo,传入按钮的值判断是否全选
    checkAllTodo(done) {
      this.todos.forEach(todo => {
        todo.done = done
      })
    },
    // 清除所有已完成的todo
    deleteAllTodo() {
      this.todos = this.todos.filter(todo => {
        return !todo.done
      })
    }
  }
}
</script>

<style lang="less" scoped>
.todo-wrap {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}
</style>
