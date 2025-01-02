<script setup>
// import { defineNuxtComponent } from "#app"; //

// Composition API - the reactive data wraps the value inside an object
// In tempalte section, vue automatically unwraps refs when they are accessed making it more intuitive(Easer for human)
import { ref, computed } from "vue";

const todoList = ref([]);

const completedItems = computed(() => {
    return todoList.value.filter((item) => item.completed);
});

const remainingItems = computed(() => {
    return todoList.value.filter((item) => !item.completed);
});

const fetchTodoData = () => {
    fetch("https://jsonplaceholder.typicode.com/todos/")
        // then(onFulfilled, onRejected) to handle the result of the promise
        .then((response) => response.json()) // parse the json string into js object
        .then(
            (json) => (todoList.value = json), //after the parsed it becomes a resolve promise, it can be named anything ex. json, data, result dll
        )
        .catch((error) => console.log("error : " + error));
};

// Option API
// export default defineNuxtComponent({
//     data: () => ({
//         todoList: [],
//     }),
//     computed: {
//         completedItems() {
//             // Filter the todoList as an item that is completed
//             return this.todoList.filter((item) => item.completed);
//         },
//         remainingItems() {
//             // Filter the todoList as an item that is completed
//             return this.todoList.filter((item) => !item.completed);
//         },
//     },
//     methods: {
//         fetchTodoData() {
//             // fetch return a promise
//             fetch("https://jsonplaceholder.typicode.com/todos/")
//                 // then(onFulfilled, onRejected) to handle the result of the promise
//                 .then((response) => response.json()) // parse the json string into js object
//                 .then(
//                     (json) => (this.todoList = json), //after the parsed it becomes a resolve promise, it can be named anything ex. json, data, result dll
//                 )
//                 .catch((error) => console.log("error : " + error));
//         },
//     },
// });
</script>

<template>
    <div class="section">
        <p>
            Photo by
            <a
                href="https://unsplash.com/@dlxmedia?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash"
            >
                dlxmedia.hu
            </a>
            on
            <a
                href="https://unsplash.com/photos/a-laptop-and-a-charger-l7idyRTQePY?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash"
            >
                Unsplash
            </a>
        </p>
        <h1 class="title">Hello world nuxt js 3</h1>
        <button class="button" @click="fetchTodoData">Fetch data</button>
        <p>
            {{ completedItems.length }} items completed |
            {{ remainingItems.length }} remaining items
        </p>
        <ul class="list">
            <li v-for="todo in todoList" :key="`todo-id-${todo.id}`">
                <input type="checkbox" :checked="todo.completed" />
                {{ todo.title }}
            </li>
        </ul>
    </div>
</template>

<style lang="scss">
@import "./node_modules/bulma/bulma.scss";
@import "./assets/styles/main.scss";

:root {
    --text-color: #{$textColor};
}
.title {
    color: var(--text-color);
}

.list {
    color: var(--text-color);
    display: grid;
    grid-template-columns: repeat(2, 1fr);
}
</style>
