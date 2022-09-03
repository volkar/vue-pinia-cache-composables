# Vue/Pinia cache composables

Provides way of retrieving data from backend/api with caching.

- Using pinia for store responses and promises while they are in pending state
- One time backend request, all next requests will be handled by the same promise, or by the cache data if it fetched already
- Resolved promises will be removed from store

# Install ky
It uses [ky](https://github.com/sindresorhus/ky) for fetching data, can be replaced by any other datafetcher of your choice.
For use with ky you need to install it in your project:

```shell
npm install ky
```

# Install Pinia
```shell
npm install pinia
```

# Usage
Copy files from **use** and **stores** to your vue project.
Simple example located in **example.vue** file.
Second argument in **useGetRequest** is a cache key, if not set - no caching will be used.

```vue
<script setup lang="ts">
import { ref } from "vue";
import { useGetRequest } from "@/use/useFetchRequest";

const url = ref('/path/to/api')

const data = ref()
const error = ref()
const isLoading = ref(true)

useGetRequest(url, url).then((result) => {
    data.value = result
}).catch((err) => {
    error.value = err
}).finally(() => {
    isLoading.value = false
})
</script>

<template>
    <div v-if="isLoading">Loading...</div>
    <div v-else-if="error">
        Error: {{ error.message }}
    </div>
    <div v-else-if="data">
        <h1>{{ data.title }}</h1>
        <div v-html="data.content"></div>
    </div>
</template>
```

# Contact me

You always welcome to mail me at sergey@volkar.ru