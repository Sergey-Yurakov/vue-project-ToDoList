<template>
  <form @submit.prevent="onSubmit">
    <input type="text" v-model="title" />
    <button type="submit">Create</button>
  </form>
</template>

<script>
export default {
  name: "AddTodo",
  data() {
    return {
      title: "",
    };
  },
  methods: {
    onSubmit() {
      // проверяем строку из инпута на пустоту и создаем новый объект, куда кладем значения
      if (this.title.trim()) {
        const newTodo = {
          id: Date.now(),
          title: this.title,
          completed: false,
        };
        //сообщаем app компоненту, что у нас что-то изменилось
        this.$emit("add-todo", newTodo);
        this.title = '';
      }
    },
  },
};
</script>

<style scoped>
form {
  display: flex;
  justify-content: center;
}
input {
  width: 400px;
  margin-right: 1rem;
}
button {
  border: 1px solid grey;
  border-radius: 15px;
  cursor: pointer;
}
</style>