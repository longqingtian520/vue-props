<template>
  <div class="todo-container">
    <div class="todo-wrap">
      <TodoHeader @addItem="addItem"/> <!-- 给todoheader标签对象绑定addItem事件监听-->
      <TodoList :todos="todos" :deleteItem="deleteItem"/>
      <TodoFooter :todos="todos" :deleteCompleteItem="deleteCompleteItem" :isAllCheck="isAllCheck"/>
    </div>
  </div>
</template>

<script>
  import HelloWorld from './components/HelloWorld'
  import TodoFooter from './components/TodoFooter'
  import TodoHeader from './components/TodoHeader'
  import TodoList from './components/TodoList'

  export default {
    name: 'App',
    components: {
      HelloWorld,
      TodoHeader,
      TodoList,
      TodoFooter
    },
    data () {
      return {
        todos: JSON.parse(window.localStorage.getItem('todo_key') || '[]')
      }
    },
    methods: {
      addItem (todo) {
        this.todos.unshift(todo)
      },
      deleteItem (index) {
        this.todos.splice(index, 1)
      },
      deleteCompleteItem () {
        this.todos = this.todos.filter(todo => !todo.complete)
      },
      isAllCheck (check) {
        if (check) {
          this.todos.forEach(todo => todo.complete = true)
        } else {
          this.todos.forEach(todo => todo.complete = false)
        }
      }
    },
    watch: { // 监视
      todos: {
        deep: true, // 深度监视
        handler: function (value) {
          window.localStorage.setItem('todo_key', JSON.stringify(value))
        }
      }
    }
  }
</script>

<style>
  .todo-container {
    width: 600px;
    margin: 0 auto;
  }

  .todo-container .todo-wrap {
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
  }
</style>
