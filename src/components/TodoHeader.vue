<template>
  <div class="todo-header">
    <input type="text" placeholder="请输入你的任务名称，按回车键确认" v-model="title" @keyup.enter="add" />
  </div>
</template>

<script>
import { nanoid } from 'nanoid'
export default {
  name: 'Header',
  props: ['addTodo'],
  data() {
    return {
      title: ''
    }
  },
  methods: {
    add() {
      if (!this.title.trim()) {
        alert('输入不能为空')
        return false
      }
      const todo = { id: nanoid(), title: this.title, done: false }
      this.addTodo(todo)
      this.title = ''
    }
  }
}
</script>

<style lang="less" scoped>
.todo-header {
  margin: 20px 0;
  input {
    width: 560px;
    height: 38px;
    box-sizing: border-box;
    font-size: 14px;
    border: 1px solid #ccc;
    border-radius: 4px;
    padding: 4px 7px;
    &:focus {
      outline: none;
      border: none;
      box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 8px rgba(176, 176, 176, 0.6);
    }
  }
}
</style>
