<template>
  <div class="todo-container">
    <div class="todo-wrap">
      <TodoHeader @addItem="addItem"/> <!-- 给todoheader标签对象绑定addItem事件监听-->
      <TodoList :todos="todos" :deleteItem="deleteItem"/>
      <TodoFooter >
        <input type="checkbox" v-model="allCheck" slot="allcheck"/>
        <span slot="size">已完成{{completeSize}} / 全部{{this.todos.length}}</span>
        <button  class="btn btn-danger" @click="deleteFinished" v-show="completeSize" slot="delete">清除已完成任务</button>
      </TodoFooter>
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
    computed: {
      completeSize () {
        return this.todos.reduce((preNum, todo) => preNum + (todo.complete ? 1 : 0), 0)
      },
      allCheck: {
        get () {
          return this.completeSize == this.todos.length && this.completeSize > 0
        },
        set (value) { // value是CheckBox最新的值
          this.isAllCheck(value)
        }
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
      },
      deleteFinished () {
        if (window.confirm('确定要清除已完成的任务吗？')) {
          this.deleteCompleteItem()
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
