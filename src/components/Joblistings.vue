<script setup>
import { ref } from 'vue'
import jobData from '@/jobs.json'

const jobs = ref(jobData)
</script>

<template>
    Job listing
    <div v-for="job in jobs.value" :key="job.id">
        {{ job.title }}
    </div>
    <!-- <section class="bg-blue-50 px-4 py-10">
        <div v-for="job in jobs" :key="job.id">
            {{ job.title }}
        </div>
    </section> -->
</template>