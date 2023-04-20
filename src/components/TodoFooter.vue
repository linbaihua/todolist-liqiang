<template>
  <div class="todo-footer">
    <label>
      <input type="checkbox" v-model="isAll" />
      <span>已完成{{ doneTotal }} / 全部{{ total }}</span>
    </label>
    <button @click="clearAll">清除已完成任务</button>
  </div>
</template>

<script>
export default {
  name: 'TodoFooter',
  props: [ 'todos', 'checkAllTodo',  'clearAllTodo' ],
  computed: {
    total() {
      return this.todos.length
    },
    doneTotal() {
      return this.todos.reduce((pre, todo) => pre + (todo.done ? 1 : 0), 0)
    },
    //控制全选框
    isAll: {
      //全选框是否勾选
      get() {
        return this.doneTotal === this.total && this.total > 0
      },
      //isAll被修改时set被调用
      set(value) {
        this.checkAllTodo(value)
      }
    }
  },
  methods: {
    clearAll() {
      // this.todos = this.todos.filter(todo => !todo.done)
      this.clearAllTodo()
    }
  }
}
</script>

<style lang="less" scoped>
.todo-footer {
  margin-top: 10px;
  display: flex;
  justify-content: space-between;
  label {
    padding-left: 10px;
  }
  button {
    margin-right: 20px;
  }
}
</style>
