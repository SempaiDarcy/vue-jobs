<script setup>
import jobData from '@/jobs.json'
import {ref} from 'vue'

const jobs = ref(jobData)
console.log(jobData)
</script>
<template>
  Job Listings
</template>
