<template>
    <div id="app">
        <Header />
        <!-- angular router-outlet in vue is called router-view  -->
        <router-view />
    </div>
</template>

<script>
import Header from "./components/layout/Header";

export default {
    name: "App",
    // all components that we want to use in current component should be imported and
    // placed in components property (listing imported components)
    components: { Header },
    data() {
        return {
            todos: [],
        };
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

.btn :hover {
    background: #666;
}
</style>
