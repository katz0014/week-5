<template>
  <div>
    <h1>Todo List</h1>
    <h2 slot="name">Add A Todo</h2>
    <TodoForm @newTodo="addTodo" />
    <p slot="desc">Your Todo</p>
    <Todo :Todos="TodoList" @removeTodo="appDeleteTodo" />
  </div>
</template>
<script>
import Todo from "@/components/Todo.vue";
import TodoForm from "@/components/TodoForm.vue";
import axios from "axios";
export default {
  data() {
    return {
      TodoList: []
    };
  },
  components: {
    Todo,
    TodoForm
  },
  methods: {
    appDeleteTodo(index) {
      this.TodoList.splice(index, 1);
      axios.put(
        "https://katz0014-vue-and-axios.firebaseio.com/data.json",
        this.Todolist
      );
    },
    addTodo(todo) {
      this.TodoList.push(todo);
      axios
        .put(
          "https://katz0014-vue-and-axios.firebaseio.com/data.json",
          this.TodoList
        )
        .then(response => {
          console.log(response);
          console.log("Your data was saved status: " + response.status);
        })
        .catch(error => {
          console.log(error);
        });
    }
  },
  beforeCreate() {
    console.log("before app is created");
  },
  created() {
    axios
      .get("https://katz0014-vue-and-axios.firebaseio.com/data.json")
      .then(response => {
        console.log(response.data);
        this.Todolist = response.data;
        if (response.data) {
          this.Todolist = response.data;
        }
      })
      .catch(error => {
        console.log("there was an error in getting data: " + error.response);
      });
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
