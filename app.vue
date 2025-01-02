<script>
import { defineNuxtComponent } from "#app"; //

export default defineNuxtComponent({
    data: () => ({
        todoList: [],
    }),
    methods: {
        fetchTodoData() {
            // fetch return a promise
            fetch("https://jsonplaceholder.typicode.com/todos/")
                // then(onFulfilled, onRejected) to handle the result of the promise
                .then((response) => response.json()) // parse the json string into js object
                .then(
                    (json) => (this.todoList = json), //after the parsed it becomes a resolve promise, it can be named anything ex. json, data, result dll
                )
                .catch((error) => console.log("error : " + error));
        },
    },
});
</script>

<template>
    <div>
        <img src="/todo.jpg" alt="Todo photo by dlxmedia.hu" />
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
        <h1>Hello world nuxt js 3</h1>
        <button @click="fetchTodoData">Fetch data</button>
        <ul>
            <li v-for="todo in todoList" :key="`todo-id-${todo.id}`">
                <input type="checkbox" :checked="todo.completed" />
                {{ todo.title }}
            </li>
        </ul>
    </div>
</template>
