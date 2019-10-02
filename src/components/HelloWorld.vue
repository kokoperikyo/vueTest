<template>
  <div>
    {{ msg }}
    <form>
      <button @click="addTodo()" >ADD TASK</button>
      <button @click="removeTodo()">DELETE FINISHED TASKS</button>
      <p>input: <input type="text" v-model="newTodo"></p>
      <p>task: {{ newTodo }}</p>
    </form>
    <div class="task-list">
      <label class="item" v-for="todo in todos" v-bind:class="{ 'checked': todo.done }">
        <input type="checkbox" v-model="todo.done">
        <input type="checkbox" v-model="todo.editing">
        <input v-if="todo.editing" v-model="todo.text" @keyup.enter="todo.editing = !todo.editing">
        <span v-else>{{ todo.text }}</span>
      </label>
    </div>
  </div>
</template>

<script>
export default {
  name: 'hello',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      todos : [
        {text : 'task1', done: false, editing: false},
        {text : 'task2', done: false, editing: false},
        {text : 'task3', done: false, editing: false},
        {text : 'task4', done: true, editing: false},
      ],
      newTodo: ""
    }
  },  
  methods: {
    addTodo: function(event) {
      let inputtext = this.newTodo && this.newTodo.trim()
      if (!inputtext) {
        return
      }
      this.todos.push({
        text: inputtext,
        done: false,
        editing: false
      })
      this.newTodo = ''
    },
    removeTodo: function (event) {
      for (let i = this.todos.length - 1; i >= 0; i--) {
        if (this.todos[i].done) this.todos.splice(i, 1)
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="css" scoped>

.task-list {
  display: flex;
  flex-direction: column;
  align-items: center;
} 

.task-list .item{
  width: 270px;
  text-align: left;
}

.checked{
  color: aqua;
}
</style>