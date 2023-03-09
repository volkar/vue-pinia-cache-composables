# Vue/Pinia cache composables

Provides way of retrieving data from backend/api with caching.

- Using pinia for store responses and promises while they are in pending state
- One time backend request, all next requests will be handled by the same promise, or by the cache data if it fetched already
- Custom expiration time for each request forcing to refetch data when expired
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
There is two functions in useApi.<br>
First one - getApi(), will use get request with no any caching.<br>
Second one - getApiWithCache(), will use get request with caching with expiration time defined in second argument 

```vue
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
```

# Contact me

You always welcome to write me
- E-mail: sergey@volkar.ru
- Telegram: @sergeyvolkar