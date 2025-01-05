<script setup>
// import { defineNuxtComponent } from "#app"; //

// Composition API - the reactive data wraps the value inside an object
// In tempalte section, vue automatically unwraps refs when they are accessed making it more intuitive(Easer for human)
import { ref, computed, onMounted } from "vue";
import { useRoute } from "vue-router";

const todoList = ref([]);
const route = useRoute();

const completedItems = computed(() => {
    return todoList.value.filter((item) => item.completed);
});

const remainingItems = computed(() => {
    return todoList.value.filter((item) => !item.completed);
});

const filterTodo = computed(() => {
    if (route.query.completed === undefined) {
        return todoList.value;
    }

    const query = route.query.completed === "true";

    return todoList.value.filter((item) => item.completed === query);
});

onMounted(() => {
    fetch("https://jsonplaceholder.typicode.com/todos/")
        // then(onFulfilled, onRejected) to handle the result of the promise
        .then((response) => response.json()) // parse the json string into js object
        .then(
            (json) => (todoList.value = json), //after the parsed it becomes a resolve promise, it can be named anything ex. json, data, result dll
        )
        .catch((error) => console.log("error : " + error));
});

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
    <NuxtPage v-if="route.params.id" />
    <BaseViewer v-else class="space-y-5" title="Todo Viewer">
        <template v-slot:heading>
            <p>
                {{ completedItems.length }} items completed |
                {{ remainingItems.length }} remaining items |
                {{ filterTodo.length }} listed
            </p></template
        >
        <template v-slot:content>
            <ul class="grid grid-cols-2">
                <li v-for="todo in filterTodo" :key="`todo-id-${todo.id}`">
                    <NuxtLink :to="`/display/todo/${todo.id}`"
                        ><UCheckbox
                            :model-value="todo.completed"
                            :label="todo.title"
                    /></NuxtLink>
                </li>
            </ul>
        </template>
    </BaseViewer>
</template>
