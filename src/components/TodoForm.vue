<template>
    <form @submit.prevent>
        <h4>Створити задачу </h4>
        <input
            v-model.trim="todo.author"
            class="input"
            type="text" 
            placeholder="Автор"
        >
        <input
            v-model.trim="todo.body"
            class="input"
            type="text" 
            placeholder="Яка задача?"
        >
        <my-button
            style="margin-top: 15px;"
            @click="createTodo"
        >Створити</my-button>
    </form>  
</template>

<script>
export default {
    data() {
        return {
            todo: {
                author: '',
                body: ''
            }
        }
    },

    methods: {
        createTodo() {
            if (this.todo.author && this.todo.body) {
                this.todo.id = Date.now();
                this.$emit('create', this.todo);
                this.todo = {
                    title: '',
                    body: ''
                };
            } else {
                alert("Заповніть будь ласка всі поля")
            }
        },
    }
}
</script>

<style scoped>
form {
    padding: 20px;
    display: flex;
    flex-direction: column;
}

.input {
    width: 100%;
    border: 2px solid teal;
    margin-top: 15px;
    padding: 15px;
}
</style>