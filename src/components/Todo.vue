<template>
  <ul>
    <li v-for="(Todo, index) in Todos" :key="index" @click="todoDone(index)">
      {{ Todo }}
    </li>
  </ul>
</template>
<script>
export default {
  props: {
    Todos: {
      type: Array,
      required: true
    }
  },
  methods: {
    todoDone(index) {
      console.log(index);
      // $emit emits an event from the child component to the parent component
      this.$emit("removeTodo", index);
    }
  }
};
</script>
