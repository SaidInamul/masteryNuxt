<script setup>
import { useRoute } from "vue-router";

useHead({
    title: "Pokemon ID : ",
});

const route = useRoute();
</script>

<template>
    <h1 class="font-medium">This is pokemon id : {{ route.params.id }}</h1>
</template>
