<template>
<<<<<<< HEAD
  <div>
    <h2>第一个Vue组件化项目</h2>
    <img src="./assets/logo.png" alt="logo" class="logo"/>
    <HelloWorld/>
=======
  <div class="todo-container">
    <div class="todo-wrap">
      <TodoHeader @addTodo="addTodo"/>
      <TodoMain :todos="todos"/>
      <TodoFooter>
        <input type="checkbox" v-model="isCheckAll" slot="check"/>
        <span slot="size">已完成{{completeSize}}/ 全部{{todos.length}}</span>
        <button class="btn btn-danger" v-show="completeSize" @click="deleteCompleteTodos" slot="delete">清除已完成任务</button>
      </TodoFooter>
    </div>
>>>>>>> Vue
  </div>
</template>

<script>
<<<<<<< HEAD
  import HelloWorld from './compontents/HelloWorld.vue'

  export default {
    components: {
        HelloWorld
=======
  import PubSub from 'pubsub-js'
  import Header from './components/Header.vue'
  import Main from './components/Main.vue'
  import Footer from './components/Footer.vue'
  import storageUtils from './utils/storageUtils'

  export default {

    data () {
      return {
        todos: storageUtils.readTodos()
      }
    },

    computed: {
      // 完成的数量
      completeSize () {
        return this.todos.reduce((pre, todo) => pre + (todo.complete ? 1 : 0), 0)
      },
      // 是否选择/同步修改所有todo
      isCheckAll: {
        get () {
          return this.todos.length===this.completeSize && this.completeSize>0  // 计算属性的函数不能调用
        },

        set (value) { // value代表当前是否勾选的boolean值
          this.selectAllTodos(value)
        }
      }
    },

    mounted () {
      // 订阅消息(deleteTodo)
      PubSub.subscribe('deleteTodo', (msg, index) => {
        this.deleteTodo(index)
      })
    },

    methods: {
      // 添加todo
      addTodo (todo) {
        this.todos.unshift(todo)
      },

      // 删除指定下标的todo
      deleteTodo (index) {
        this.todos.splice(index, 1)
      },

      // 删除已完成的todo
      deleteCompleteTodos () {
        this.todos = this.todos.filter(todo => !todo.complete)
      },

      // 全选或全不选所有todo
      selectAllTodos (isCheck) {
        this.todos.forEach(todo => todo.complete = isCheck)
      }

    },

    watch: {
      todos: {
        deep: true,
        handler: storageUtils.saveTodos
      }
    },

    components: {
      TodoHeader: Header,
      TodoMain: Main,
      TodoFooter: Footer,
>>>>>>> Vue
    }
  }
</script>

<style>
<<<<<<< HEAD
  .logo {
    width: 100px;
    height: 100px;
  }


=======
  .todo-container {
    width: 600px;
    margin: 0 auto;
  }
  .todo-container .todo-wrap {
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
  }
>>>>>>> Vue
</style>
