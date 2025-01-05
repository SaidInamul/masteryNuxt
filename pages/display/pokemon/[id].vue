<script setup>
import { useRoute } from "vue-router";
import { defineProps } from "vue";

const route = useRoute();
useHead({ title: `Pokemon-${route.params.id}` });
</script>

<template>
    <h1 class="font-medium">This is pokemon id : {{ route.params.id }}</h1>
</template>
