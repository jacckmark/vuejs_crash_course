<template>
    <div>
        <!-- onsubmit we will call the method addTodo from component methods property -->
        <form @submit="addTodo">
            <!-- v-model is a two way data binding which will update variable title
            (thus we will be able to use it like "this.title" when needed) -->
            <input v-model="title" type="text" name="title" placeholder="Add Todo..." />
            <input type="submit" value="Submit" class="btn" />
        </form>
    </div>
</template>

<script>
export default {
    name: "AddTodo",
    // defining the component data (here empty variable title)
    data() {
        return {
            title: "",
        };
    },
    // component methods
    methods: {
        addTodo(e) {
            // this will ensure that form will not submit and thus reload itself
            // which is a default form submition behauviour
            e.preventDefault();
            // assigning the title collected from form with v-model to obj and default
            // value for completed property
            const newTodo = {
                title: this.title,
                completed: false,
            };
            // we are emmiting the event called add-todo with newTodo object attached
            this.$emit("add-todo", newTodo);
            // resetting the title value (thus also removing it from a form, thanks
            // to two way data binding)
            this.title = "";
        },
    },
};
</script>

<style>
form {
    display: flex;
}

input[type="text"] {
    flex: 10;
    padding: 5px;
}

input[type="submit"] {
    flex: 2;
}
</style>
