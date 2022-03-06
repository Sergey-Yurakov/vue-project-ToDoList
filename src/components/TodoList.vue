<template>
    <div>
        <ul>
            <!-- v-bind:key коротко это просто :key -->
            <!-- v-on:click коротко это просто @click -->
            <TodoItem 
            v-for="(item,i) in todos" :key="item.id" 
            :item="item"
            :index='i'
            @remove-todo = "removeTodo" 
            />
        </ul>
    </div>
</template>




<script>
import TodoItem from "@/components/TodoItem.vue";
export default {
    name: "TodoList",
    props: ["todos"],
    components: {
        TodoItem,
    },
    methods: {
        removeTodo(id) {
            this.$emit('remove-todo', id)
        } 
    }
};
</script>

<style scoped>
ul {
    list-style: none;
    margin: 0;
    padding: 0;
}
</style>