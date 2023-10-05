<script setup>
import { inject } from 'vue';
const topMsg = inject('topMsg')
const topWeek = inject('topWeek')
const commit = inject('commited')
</script>
<template>
    <p>From App directly: {{ topMsg }}</p>
    <ul>
        <li v-for="(item,key,index) of topWeek" :key="index">{{ key }} - {{ item }}</li>
    </ul>
    <button @click="commit">COMMIT</button>
</template>