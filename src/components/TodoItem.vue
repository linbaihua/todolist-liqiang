<template>
  <li>
    <label>
      <input type="checkbox" :checked="todo.done" @change="handleCheck(todo.id)" />
      <span>{{ todo.title }}</span>
    </label>
  </li>
</template>

<script>
export default {
  name: 'TodoItem',
  props: ['todo', 'checkTodo', 'deleteTodo'],
  methods: {
    handleCheck(id) {
      //通知App组件将对应的todo对象的done值取反
      this.checkTodo(id)
    },
    handleDelete(id) {
      if (confirm('确定删除吗？')) {
        //通知App组件将对应的todo对象删除
        this.deleteTodo(id)
      }
    }
  }
}
</script>

<style lang="less" scoped></style>
