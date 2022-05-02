<template>
    <div>
        <transition-group name="todo-list">
            <todo-item 
                v-for="todo in todos"
                :todo="todo"
                :key="todo.id"
                @delete="this.$emit('delete', todo)"
            />
        </transition-group>
    </div>
</template>

<script>
import TodoItem from "@/components/TodoItem.vue"
export default {
    components: {
        TodoItem
    },

    props: {
        todos: {
            type: Array,
            required: true,
        }
    }
};
</script>

<style scoped>
h3 {
    margin: 15px 15px;

}

.todo-list-item {
  display: inline-block;
  margin-right: 10px;
}

.todo-list-enter-active,
.todo-list-leave-active {
  transition: all 1s ease;
}

.todo-list-enter-from,
.todo-list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}

.todo-list-move {
  transition: transform 0.8s ease;
}
</style>