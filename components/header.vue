<script setup></script>

<template>
    <nav class="bg-green-400 dark:bg-gray-900">
        <div
            class="max-w-screen-xl flex flex-wrap items-center justify-between mx-auto p-4"
        >
            <NuxtLink to="/" class="font-thin flex items-center space-x-2">
                <img src="/logo.png" class="h-8" alt="Logo" />
                <p class="">
                    Sandbox
                    <span class="text-lg font-medium dark:text-white">
                        Nuxt</span
                    >
                </p>
            </NuxtLink>
            <div class="hidden w-full md:block md:w-auto" id="navbar-default">
                <ul
                    class="flex flex-col md:flex-row md:space-x-8 rtl:space-x-reverse md:mt-0 dark:bg-gray-800 md:dark:bg-gray-900 dark:border-gray-700"
                >
                    <li>
                        <NuxtLink
                            to="/"
                            class="block font-semibold md:text-gray-800 dark:text-white md:dark:text-blue-500"
                            aria-current="page"
                            >Home</NuxtLink
                        >
                    </li>
                    <li>
                        <NuxtLink href="/display" class="block text-gray-800"
                            >Display</NuxtLink
                        >
                    </li>
                    <li>
                        <NuxtLink
                            href="/display/pokemon"
                            class="block text-gray-800"
                            >Pokemon</NuxtLink
                        >
                    </li>
                    <li>
                        <NuxtLink
                            href="/display/todo"
                            class="block text-gray-800"
                            >Todo</NuxtLink
                        >
                    </li>
                </ul>
            </div>
        </div>
    </nav>
</template>
