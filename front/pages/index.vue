<template>
  <div v-if="user"> <!-- v-ifを追加 -->
    <p>名前：{{user.name}}</p>
    <p>メール{{user.email}}</p>
    <AddTodo @submit="addTodo" />
    <TodoList :todos="todos" />
  </div>
</template>

<script>
  import AddTodo from "@/components/AddTodo";
  import TodoList from "@/components/TodoList";
  import axios from "@/plugins/axios";  // 追加

  export default {
    components: {
      AddTodo,
      TodoList,
    },
    data() {
      return {
        todos: [],
      };
    },
    // ここから追加
    computed: {
      user() {
        return this.$store.state.auth.currentUser;
      }
    },
    // ここまで追加
    created() {
      console.log("API_KEY:", process.env.API_KEY);
    },
    methods: {
      async addTodo(title) {
        await axios.post("/v1/todos", { title })
        this.todos.push({
          title
        });
      },
    },
  };
</script>