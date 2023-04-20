<template>
  <li>
    <label>
      <input type="checkbox" :checked="todo.done" @change="handleCheck(todo.id)" />
      <span v-show="!todo.isEdit">{{ todo.title }}</span>
      <input type="text" ref="inputTitle" v-show="todo.isEdit" :value="todo.title" @blur="handleBlur(todo, $event)" />
    </label>
    <div class="btn-container">
      <button v-show="!todo.isEdit" class="btn edit" @click="handelEdit(todo)">编辑</button>
      <button class="btn delete" @click="handleDelete(todo.id)">删除</button>
    </div>
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
    },
    // 编辑
    handelEdit(todo) {
      if (todo.hasOwnProperty('isEdit')) {
        todo.isEdit = true
      } else {
        this.$set(todo, 'isEdit', true)
      }
      // isEdit在本次DOM中是没有的，然后在下次DOM 更新给它加上
      // 那么这个时候要基于 isEdit 的操作在这次更新是无效的
      // 使用 nextTick 将回调函数在页面渲染完新的数据后再执行操作就有效了
      this.$nextTick(function () {
        this.$refs.inputTitle.focus()
      })
    },
    // 失去焦点事件
    handleBlur(todo, e) {
      todo.isEdit = false
      if (!e.target.value.trim()) {
        alert('输入不能为空')
        return false
      }
      this.$bus.$emit('updateTodo', todo.id, e.target.value)
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
  justify-content: space-between;
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
  .btn-container {
    display: flex;
    .btn {
      height: 30px;
      width: 50px;
      background-color: rgba(255, 73, 73, 0.856);
      border: none;
      border-radius: 3px;
    }
    .delete {
      margin-right: 10px;
      margin-left: 5px;
    }
  }
}
</style>
