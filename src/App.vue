<template>
  <div id="app">
    <div class="todo-container">
      <div class="todo-wrap">
        <h2>TodoList</h2>
        <TodoHeader :addTodo="addTodo" />
        <todo-list :todos="todos" :checkTodo="checkTodo" :deleteTodo="deleteTodo" />
        <TodoFooter :todos="todos" :checkAllTodo="checkAllTodo" :clearAllTodo="clearAllTodo" />
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
      todos: JSON.parse(localStorage.getItem('todos')) || []
    }
  },
  methods: {
    // 添加一个todo,传入一个todo对象
    addTodo(todo) {
      this.todos.unshift(todo)
    },
    // 删除一个todo
    deleteTodo(id) {
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
    clearAllTodo() {
      this.todos = this.todos.filter(todo => {
        return !todo.done
      })
    },
    //更新一个todo
    updateTodo(id, title) {
      this.todos.forEach(todo => {
        if (todo.id === id) todo.title = title
      })
    }
  },
  watch: {
    todos: {
      deep: true,
      handler(value) {
        localStorage.setItem('todos', JSON.stringify(value))
      }
    }
  }
}
</script>

<style lang="less" scoped>
.todo-container {
  width: 580px;
  margin: 100px auto;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
  display: flex;
  justify-content: center;
  align-items: center;
  .todo-wrap {
    width: 560px;
    h2 {
      width: 560px;
      margin: 10px 0;
      text-align: center;
      background-color: #eeeded;
      border-radius: 5px;
    }
  }
}
</style>
