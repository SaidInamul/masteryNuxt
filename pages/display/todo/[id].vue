<script setup>
import { useRoute } from "vue-router";

const route = useRoute();

useHead({ title: `Todo-${route.params.id}` });
</script>

<template>
    <h1 class="font-medium">This is todo id : {{ route.params }}</h1>
</template>
