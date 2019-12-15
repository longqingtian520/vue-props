<template>
  <div class="todo-header">
    <input type="text" placeholder="请输入你的任务名称，按回车键确认" v-model="title" @keyup.enter="add"/>
  </div>
</template>

<script>
  export default {
    name: 'TodoHeader',
    // props: {
    //    addItem: {
    //     type: Function,
    //     required: true
    //   }
    // },
    data () {
      return {
        title: ''
      }
    },
    methods: {
      add () {
        // 检查输入的合法性
        const title = this.title.trim()
        if (!title) {
          alert('请输入合法数据')
          return
        }
        // 根据输入生成一个todo对象
        const todo = {title, complete: false}

        // 添加到todos
        // this.addItem(todo)
        this.$emit('addItem', todo)
        // 清除输入
        this.title = ''
      }
    }
  }
</script>

<style scoped>
  .todo-header input {
    width: 560px;
    height: 28px;
    font-size: 14px;
    border: 1px solid #ccc;
    border-radius: 4px;
    padding: 4px 7px;
  }

  .todo-header input:focus {
    outline: none;
    border-color: rgba(82, 168, 236, 0.8);
    box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 8px rgba(82, 168, 236, 0.6);
  }
</style>
