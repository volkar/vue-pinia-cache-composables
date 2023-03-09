<script setup lang="ts">
    import { onMounted } from 'vue'
    import useApi from '@/use/useApi'

    // Get api data
    const { data, isLoading, isLoaded, errors, getApiWithCache } = useApi()
    onMounted(() => {
        // Get data from api with cache time of 300 seconds
        getApiWithCache('getsomedata', 300)
    })
</script>

<template>
    <div v-if="isLoading && !isLoaded">
        Loading...
    </div>
    <div v-if="errors && !isLoading">
        Ooops!<br>
        {{ errors }}
    </div>
    <div v-if="isLoaded && !errors">
        <h1>{{ data.title }}</h1>
        <div v-html="data.content"></div>
    </div>
</template>