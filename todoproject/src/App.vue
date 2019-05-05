<template>
  <div id="app">
    <Header></Header>
    <Input v-on:addTodo="addTodo"></Input>
    <List v-bind:propsdata="todoItems" @removeTodo="removeTodo"></List>
    <Footer v-on:removeAll="clearAll"></Footer>
  </div>
</template>

<script>
  import Header from './components/header'
  import Input from './components/Input'
  import List from './components/List'
  import Footer from './components/Footer'

  export default {
    data() {
      return {
        todoItems: []
      }
    },
    methods: {
      addTodo(todoItem) {
        localStorage.setItem(todoItem, todoItem);
        this.todoItems.push(todoItem);
      },
      removeTodo(todoItem, index) {
        localStorage.removeItem(todoItem);
        this.todoItems.splice(index, 1);
      },
      clearAll() {
        localStorage.clear();
        this.todoItems = [];
      }
    },
    created() {
      if (localStorage.length > 0) {
        for (let i = 0; i < localStorage.length; i++) {
          this.todoItems.push(localStorage.key(i));
        }
      }
    },
    components: {
      'Header': Header,
      'Input': Input,
      'List': List,
      'Footer': Footer
    }
  }
</script>

<style>
  body {
    text-align: center;
    background-color: #F6F6F8;
  }

  input {
    border-style: groove;
    width: 200px;
  }

  button {
    border-style: groove;
  }

  .shadow {
    -webkit-box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
    -moz-box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
    box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
  }
</style>
