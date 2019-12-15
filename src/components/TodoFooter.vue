<template>
  <div class="todo-footer">
    <label>
      <input type="checkbox" v-model="allCheck"/>
    </label>
    <span>
          <span>已完成{{completeSize}}</span> / 全部{{this.todos.length}}
        </span>
    <button class="btn btn-danger" @click="deleteFinished">清除已完成任务</button>
  </div>
</template>

<script>
  export default {
    name: 'TodoFooter',
    props: {
      todos: Array,
      deleteCompleteItem: Function,
      isAllCheck: Function
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
      deleteFinished () {
        if (window.confirm('确定要清除已完成的任务吗？')) {
          this.deleteCompleteItem()
        }
      }
    }
  }
</script>

<style scoped>
  .todo-footer {
    height: 40px;
    line-height: 40px;
    padding-left: 6px;
    margin-top: 5px;
  }

  .todo-footer label {
    display: inline-block;
    margin-right: 20px;
    cursor: pointer;
  }

  .todo-footer label input {
    position: relative;
    top: -1px;
    vertical-align: middle;
    margin-right: 5px;
  }

  .todo-footer button {
    float: right;
    margin-top: 5px;
  }
</style>
