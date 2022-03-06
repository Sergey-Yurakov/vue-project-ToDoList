<template>
  <div>
    <h2>Todos</h2>
    <router-link to="/">Home</router-link>
    <hr />
    <AddTodo 
        @add-todo="addTodo" 
    />
    <!-- привязываем переменную filter к select, через модель -->
    <select v-model="filter">
        <option value="all">All</option>
        <option value="completed">Completed</option>
        <option value="not-completed">Not Completed</option>
    </select>
    <hr />
    <Loader
        v-if="loading"
    />
    <!-- затем можно указать его (компонент) уже в шаблоне -->
    <TodoList 
        v-else-if="filteredTodos.length" 
        :todos="filteredTodos" 
        @remove-todo="removeTodo" 
    />
    <p v-else>No todos!</p>
  </div>
</template>

<script>
//@ - это всегда папка src
//сперва надо сделать импорт компонента
import TodoList from '@/components/TodoList.vue';
import AddTodo from '@/components/AddTodo.vue';
import Loader from '@/components/Loader.vue'
export default {
  name: "App",
  //затем в разделе компонент надо его зарегестрировть
  data() {
    return {
      todos: [],
      loading: true,
      filter: 'all'
    };
  },
  // аналог ComponentDidMount
  mounted() {
    fetch("https://jsonplaceholder.typicode.com/todos?_limit=5")
      .then((response) => response.json())
      .then((json) => {
          //задержка, чтобы проверить работу лоадера
          setTimeout(() => {
            this.todos = json;
            this.loading = false;
          },2000)
      });
  },
//   watch: {
//       //название функции должно совпадать с названием модели !!!!
//       filter(value) {
//           console.log(value);
//       }
//   },

//вычисляемое св-во (что-то вроде аналога watch)
computed: {
    //в функциях описывают логику, которая зависит от моделей или переменных во vue
    //функции в computed являются переменными !!!!
    filteredTodos() {
        if(this.filter === 'all') {
            return this.todos;
        }

        if(this.filter === 'completed') {
            return this.todos.filter(e => e.completed)
        }

        if(this.filter === 'not-completed') {
            return this.todos.filter(e => !e.completed)
        }
    }
},
  methods: {
    removeTodo(id) {
      console.log(id);
      this.todos = this.todos.filter((elem) => elem.id !== id);
    },
    addTodo(todo) {
      this.todos.push(todo);
    },
  },
  components: {
    TodoList,
    AddTodo,
    Loader
  },
};
</script>

<style scoped>
    select {
        margin-top: 10px;
    }
</style>