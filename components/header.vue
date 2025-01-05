<script setup>
import { ref } from "vue";

const visibleTodo = ref(false);
</script>

<template>
    <nav class="bg-white border-gray-200 dark:bg-gray-900 dark:border-gray-700">
        <div
            class="max-w-screen-xl flex flex-wrap items-center justify-between mx-auto p-4"
        >
            <NuxtLink to="/" class="font-thin flex items-center space-x-2">
                <img src="/logo.png" class="h-8" alt="Logo" />
                <p class="text-green-500">
                    Sandbox
                    <span
                        class="text-lg text-black font-medium dark:text-white"
                    >
                        Nuxt</span
                    >
                </p>
            </NuxtLink>
            <div class="hidden w-full md:block md:w-auto" id="navbar-dropdown">
                <ul
                    class="flex flex-col font-medium p-4 md:p-0 mt-4 border border-gray-100 rounded-lg bg-gray-50 md:space-x-8 rtl:space-x-reverse md:flex-row md:mt-0 md:border-0 md:bg-white dark:bg-gray-800 md:dark:bg-gray-900 dark:border-gray-700"
                >
                    <li>
                        <NuxtLink to="/"
                            ><UButton color="primary" variant="soft"
                                >Home</UButton
                            ></NuxtLink
                        >
                    </li>
                    <li>
                        <NuxtLink to="/display"
                            ><UButton color="primary" variant="soft"
                                >Display</UButton
                            ></NuxtLink
                        >
                    </li>
                    <li>
                        <NuxtLink to="/display/pokemon"
                            ><UButton color="primary" variant="soft"
                                >Pokemon</UButton
                            ></NuxtLink
                        >
                    </li>
                    <li class="relative">
                        <UButton
                            icon="i-heroicons-chevron-down-16-solid"
                            size="sm"
                            color="primary"
                            variant="soft"
                            label="Todo"
                            trailing
                            @click="visibleTodo = !visibleTodo"
                        />
                        <div
                            v-if="visibleTodo"
                            id="dropdownNavbar"
                            class="absolute z-10 top-full right-0 font-normal bg-white divide-y divide-gray-100 rounded-lg shadow w-32 dark:bg-gray-700 dark:divide-gray-600"
                        >
                            <ul
                                class="py-2 text-sm text-gray-700 dark:text-gray-400"
                                aria-labelledby="dropdownLargeButton"
                            >
                                <li>
                                    <NuxtLink
                                        to="/display/todo"
                                        class="block px-4 py-2 hover:bg-green-100 hover:text-green-500 dark:hover:bg-green-600 dark:hover:text-white"
                                        >List todo</NuxtLink
                                    >
                                </li>
                                <li>
                                    <NuxtLink
                                        to="/display/todo?completed=true"
                                        class="block px-4 py-2 hover:bg-green-100 hover:text-green-500 dark:hover:bg-green-600 dark:hover:text-white"
                                        >Completed</NuxtLink
                                    >
                                </li>
                                <li>
                                    <NuxtLink
                                        to="/display/todo?completed=false"
                                        class="block px-4 py-2 hover:bg-green-100 hover:text-green-500 dark:hover:bg-green-600 dark:hover:text-white"
                                        >Incompleted</NuxtLink
                                    >
                                </li>
                            </ul>
                        </div>
                    </li>
                </ul>
            </div>
        </div>
    </nav>
</template>
