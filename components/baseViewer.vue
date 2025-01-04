<script setup>
import { defineProps } from "vue";

const props = defineProps({
    title: {
        type: String,
        default: "Hello World Nuxt Js",
    },
});
</script>

<template>
    <div>
        <!-- Generic Template -->
        <h1 class="text-xl font-semibold">{{ title }}</h1>
        <slot name="heading" />
        <!-- <button @click="fetchItemList">Fetch Data</button> -->
        <slot name="content" />
    </div>
</template>
