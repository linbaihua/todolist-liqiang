<template>
  <div class="todo-list">
    <todo-item v-for="todo in todos" :key="todo.id" :todo="todo" :checkTodo="checkTodo" :deleteTodo="deleteTodo" />
  </div>
</template>

<script>
import TodoItem from './TodoItem.vue'
export default {
  name: 'TodoList',
  components: { TodoItem },
  props: ['todos', 'checkTodo', 'deleteTodo']
}
</script>

<style lang="less" scoped>
.todo-list {
  width: 560px;
  box-sizing: border-box;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding: 0;
}
</style>
