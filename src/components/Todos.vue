<template>
    <div>
        <!-- here angular ngfor in vuejs (we are looping over todos array) -->
        <div v-bind:key="todo.id" v-for="todo in todos">
            <!-- passing the todo (from our loop) to component props (angular input) 
          and waiting on event (del-todo) on which we will emit information up (event 
          will be called still del-todo)-->
            <TodoItem v-bind:todo="todo" v-on:del-todo="$emit('del-todo', todo.id)"></TodoItem>
        </div>
    </div>
</template>

<script>
import TodoItem from "./TodoItem";

export default {
    name: "Todos",
    components: { TodoItem },
    props: ["todos"],
};
</script>

<style scoped></style>
