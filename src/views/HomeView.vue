<script setup>
import Hero from "@/components/Hero/Hero.vue";
import JobListings from "@/components/JobListings/JobListings.vue";
import HomeCard from "@/components/HomeCards/HomeCards.vue";
</script>
<template>
  <Hero/>
  <HomeCard/>
  <JobListings :limit="3" :show-button="true"/>
</template>