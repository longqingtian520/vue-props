<template>
  <li @mouseenter="handleShow(true)" @mouseleave="handleShow(false)" :style="{background: bgColor}">
    <label>
      <input type="checkbox" v-model="todo.complete"/>
      <span>{{todo.title}}</span>
    </label>
    <button class="btn btn-danger" v-show="isShow" @click="deleteCompx">删除</button>
  </li>
</template>

<script>
  export default {
    name: 'TodoItem',
    props: {
      todo: Object,
      index: Number,
      deleteItem: Function
    },
    data () {
      return {
        bgColor: 'white', // 默认的背景颜色
        isShow: false // 按钮默认是否显示
      }
    },
    methods: {
      handleShow (isEnter) {
        if (isEnter) {
          this.bgColor = 'yellow'
          this.isShow = true
        } else {
          this.bgColor = 'white',
          this.isShow = false
        }
      },
      deleteCompx(index){
        this.deleteItem(index)
      }
    }

  }
</script>

<style >
  li {
    list-style: none;
    height: 36px;
    line-height: 36px;
    padding: 0 5px;
    border-bottom: 1px solid #ddd;
  }

  li label {
    float: left;
    cursor: pointer;
  }

  li label li input {
    vertical-align: middle;
    margin-right: 6px;
    position: relative;
    top: -1px;
  }

  li button {
    float: right;
    display: none;
    margin-top: 3px;
  }

  li:before {
    content: initial;
  }

  li:last-child {
    border-bottom: none;
  }
</style>
