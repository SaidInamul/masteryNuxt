<script setup>
// import { defineNuxtComponent } from "#app"; //

// Composition API - the reactive data wraps the value inside an object
// In tempalte section, vue automatically unwraps refs when they are accessed making it more intuitive(Easer for human)
import { ref, computed } from "vue";
import BaseViewer from "./baseViewer.vue";

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
    <BaseViewer class="space-y-5" title="Todo Viewer">
        <template v-slot:heading
            ><UButton @click="fetchTodoData" label="Fetch data"></UButton>
            <p>
                {{ completedItems.length }} items completed |
                {{ remainingItems.length }} remaining items
            </p></template
        >
        <template v-slot:content>
            <ul class="grid grid-cols-2">
                <li v-for="todo in todoList" :key="`todo-id-${todo.id}`">
                    <UCheckbox
                        :model-value="todo.completed"
                        :label="todo.title"
                    />
                </li>
            </ul>
        </template>
    </BaseViewer>
</template>
