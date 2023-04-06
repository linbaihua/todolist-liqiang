<template>
  <li>
    <label>
      <input type="checkbox" :checked="todo.done" @change="handleCheck(todo.id)" />
      <span>{{ todo.title }}</span>
    </label>
    <button class="btn btn-delete" @click="handleDelete(todo.id)">删除</button>
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
      console.log(id)
      if (confirm('确定删除吗？')) {
        //通知App组件将对应的todo对象删除
        this.deleteTodo(id)
      }
    }
  }
}
</script>

<style lang="less" scoped>
li {
  list-style: none;
  height: 36px;
  line-height: 36px;
  padding: 0 10px;
  border-bottom: 1px solid #ddd;
  display: flex;
  align-items: center;
  &:before {
    content: initial;
  }
  &:last-child {
    border-bottom: none;
  }
  &:hover {
    background-color: #ddd;
    button {
      display: block;
    }
  }
  label {
    display: flex;
  }
  button {
    height: 30px;
    margin-right: 10px;
    margin-left: auto;
  }
}
</style>
