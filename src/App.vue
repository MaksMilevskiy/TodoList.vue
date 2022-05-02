<template lang="html">
    <div class="app">
        <h2>Список задач</h2>
        <div class="create__todo">
            <my-button class="create" @click="showModal">Створити задачу</my-button>
            <input type="text" v-model="searchQuery" placeholder="Пошук за автором..">
            <my-select
                v-model="selectedSort"
                :options="sortOptions"
            />
        </div>
        <my-dialogue v-model:show="isModalVisible">
            <todo-form @create="createTodo"/>
        </my-dialogue>
        <div class="list__wrapper" v-if="isLoaded">
            <todo-list
                v-if="todos.length > 0"
                :todos="sortedAndSearchedTodos"
                @delete="deleteTodo"
            />
            <h2 v-else>Список задач пустий :(</h2>
        </div>
        <h1 v-else>Список задач завантажується... :)</h1>
        
    </div>
</template>

<script>
import TodoForm from "@/components/TodoForm.vue";
import TodoList from "@/components/TodoList.vue";
import axios from "axios";

export default {
    components: {
        TodoForm, TodoList
    },

    data() {
        return {
            todos: [],

            isModalVisible: false,
            isLoaded: false,
            selectedSort: '',
            searchQuery: '',
            sortOptions: [
                {value: "author", name: "По автору"},
                {value: "body", name: "По змісту"}
            ]
        }
    },

    methods: {
        createTodo(todo) {
            this.todos.push(todo);
            this.isModalVisible = false;
        },

        deleteTodo(todo) {
            this.todos = this.todos.filter(item => item.id !== todo.id);
        },

        showModal() {
            this.isModalVisible = true;
        },

        async fetchTodos() {
            setTimeout(() =>  {               
                axios.get('https://mocki.io/v1/35825ddb-3585-4a00-9d84-e21556b34629').then((res) => {
                    this.todos = res.data;
                    this.isLoaded = true;
                })
            }, 1000)
        }

    },

    mounted() {
        this.fetchTodos();
    },

    computed: {
        sortedTodos() {
            return [...this.todos].sort((todo1, todo2) => todo1[this.selectedSort]?.localeCompare(todo2[this.selectedSort]))
        },

        sortedAndSearchedTodos() {
            return this.sortedTodos.filter(todo => todo.author.toLowerCase().includes(this.searchQuery.toLowerCase()))
        }
    }
}
</script>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

h2, h1 {
    margin: 20px;
}

/* .create {
    margin: 20px;
} */

.create__todo {
    display: flex;
    justify-content: space-between;
    margin: 20px;
}

input {
    align-self: flex-end;
    background-color: white;
    color: teal;
    border: 1px solid teal;
    padding: 10px;
}
</style>
