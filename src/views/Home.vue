<template>
    <div class="flex justify-center p-8">
        <input class="rounded border-2 border-gray-200 w-full" type="text" placeholder="Search for meals">
    </div>
    <div class="flex justify-center space-x-1">
        <router-link class="px-2 border-gray-200 border shadow hover:scale-125 "
            :to="{ name: 'byLetter', params: { letter } }" v-for="letter of letters" :key="letter">
            {{ letter }}
        </router-link>
    </div>

    <pre>{{ ingreadiets }}</pre>
</template>

<script setup>
import { computed, onMounted, ref } from "vue";
import store from "../store";
import instanceAxios from "../axios/global.js";


const letters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'.split('');
const ingreadiets = ref([]);

onMounted(async () => {
    const response = await instanceAxios.get('/list.php?i=list');
    ingreadiets.value = response.data;
});

</script>
