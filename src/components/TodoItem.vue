<template>
    <!-- v-bind is giving us an option to assign class to element conditionally
(here class is added if todo completed property is true) -->
    <div class="todo-item" v-bind:class="{ 'is-complete': todo.completed }">
        <p>
            <!-- checking (or unchecking) the checkbox will trigger the markComplete 
            function -->
            <input type="checkbox" v-on:change="markComplete" />
            {{ todo.title }}
            <!-- clicking the delete button will result in emiting del-todo event -->
            <button @click="$emit('del-todo', todo.id)" class="del">x</button>
        </p>
    </div>
</template>

<script>
export default {
    name: "TodoItem",
    // gives us an option to pass variables (information) to component (like whole
    // todo objects here)
    props: ["todo"],
    methods: {
        // method changing the completed variable in todo item
        markComplete() {
            this.todo.completed = !this.todo.completed;
        },
    },
};
</script>

<style scoped>
.todo-item {
    background: #f4f4f4;
    padding: 10px;
    border-bottom: 1px #ccc dotted;
}
.is-complete {
    text-decoration: line-through;
}
.del {
    background: #ff0000;
    color: #fff;
    border: none;
    padding: 5px 9px;
    border-radius: 50%;
    cursor: pointer;
    float: right;
}
</style>
