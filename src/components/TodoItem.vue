<template>
    <div class="todo" :class="{done: isDone}">  
        <div>{{ todo.author }}: {{ todo.body }}</div>
        <div class="todo__btns">
            <input 
                type="checkbox" 
                v-model="isDone"
            >
            <my-button @click="this.$emit('delete', todo)">Видалити</my-button>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        todo: {
            type: Object,
            required: true,
        }
    },

    data() {
        return {
            isDone: false
        }
    }
}
</script>

<style scoped>
.todo {
    margin: 15px 15px;
    padding: 10px 15px;
    border: 2px solid teal;
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.todo__btns {
    display: flex;
    align-items: center;
    justify-content: space-around;
}

input {
    margin: 10px;
    color: teal;
}

.done {
    background-color: greenyellow;
}
</style>