<template>
    <div id="app">
        <!-- on add-todo event addTodo method will be called -->
        <AddTodo v-on:add-todo="addTodo" />
        <!-- binding the todos to todos property in todos component and also waiting
        for del-todo event (then method deleteTodo will get called) -->
        <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
    </div>
</template>

<script>
import Todos from "../components/Todos";
import AddTodo from "../components/AddTodo";
// library for making the http requests
import axios from "axios";

export default {
    name: "Home",
    components: {
        Todos,
        AddTodo,
    },
    data() {
        return {
            todos: [],
        };
    },
    methods: {
        // method for deleting an todo
        deleteTodo(id) {
            axios
                .delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
                .then(() => (this.todos = this.todos.filter((todo) => todo.id !== id)))
                .catch((err) => console.log(err));
        },
        // method for adding new todo
        addTodo(newTodo) {
            const { title, completed } = newTodo;
            axios
                .post("https://jsonplaceholder.typicode.com/todos", {
                    title,
                    completed,
                })
                .then((res) => (this.todos = [...this.todos, res.data]))
                .catch((err) => console.log(err));
        },
    },
    // this will get called when component will be already created (angular afterViewInit)
    created() {
        axios
            .get("https://jsonplaceholder.typicode.com/todos?_limit=5")
            .then((res) => (this.todos = res.data))
            .catch((err) => console.log(err));
    },
};
</script>

<style>
* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}
body {
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
}
.btn {
    display: inline-block;
    border: none;
    background: #555;
    color: #fff;
    padding: 7px 20px;
    cursor: pointer;
}
.btn:hover {
    background: #666;
}
</style>
