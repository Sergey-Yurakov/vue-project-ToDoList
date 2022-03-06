<template>
    <li>
        <!-- проверяем завершен ли элемент или нет -->
        <span :class = {done:item.completed}>
            <input type="checkbox" @change = "item.completed = !item.completed"/>
            <strong>{{ index + 1 }}</strong>
            <!-- фильтры применяются через | -->
            {{ item.title | upperCase }}
        </span>
        <button class="rm" 
            @click="$emit('remove-todo', item.id)"
        >&times;</button>
    </li>
</template>

<script>
export default {
    name: "TodoItem",
    props: {
        item: {
            type: Object,
            required: true,
        },
        index: Number
    },
    //фильтры помогают как-то трансформировать данные
    filters: {
        upperCase(value) {
            return value.toUpperCase();
        }
    }
};
</script>

<style scoped>
    li {
        border: solid 1px black;
        display: flex;
        justify-content: space-between;
        padding: .5rem 2rem;
        margin-bottom: 1rem;

    }
    .rm {
        background-color: rgb(88, 109, 228);
        color: #fff;
        border-radius: 30%;
        font-weight: bold;
        cursor: pointer;
    }
    input {
        margin-right: 1rem;
        cursor: pointer;
    }
    .done {
        text-decoration: line-through;
    }
    

</style>