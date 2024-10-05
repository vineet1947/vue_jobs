<script setup>
import { ref } from 'vue'
import jobData from '@/jobs.json'

const jobs = ref(jobData.jobs)
</script>

<template>
    <h1>Job Listings</h1>

    <div v-for="job in jobs" :key="job.id">
        {{ job.title }}
    </div>
</template>
