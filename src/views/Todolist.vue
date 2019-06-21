<template>
  <div>
    <h1>Todo List</h1>
    <TodoForm @newTodo="addTodo" />
    <h2 slot="name">Add A Todo</h2>
    <p slot="desc">Your Todo</p>
    <Todo :Todos="TodoList" @removeTodo="appDeleteTodo" />
  </div>
</template>
<script>
import Todo from "@/components/Todo.vue";
import TodoForm from "@/components/TodoForm.vue";
export default {
  data() {
    return {
      TodoList: ["Walk the dog", "Go for a ride"]
    };
  },
  components: {
    Todo,
    TodoForm
  },
  methods: {
    appDeleteTodo(index) {
      this.TodoList.splice(index, 1);
    },
    addTodo(todo) {
      this.TodoList.push(todo);
    }
  }
};
</script>
<style scoped>
ul {
  list-style: none;
  width: 50%;
  margin: 0 auto;
}
ul li {
  border-bottom: 1px solid #acacac;
  padding: 10px 0;
  margin-bottom: 10px;
}
</style>
