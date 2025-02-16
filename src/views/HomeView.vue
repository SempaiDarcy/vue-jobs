<script setup>
import Hero from "@/components/Hero/Hero.vue";
import JobListings from "@/components/JobListings/JobListings.vue";
import HomeCard from "@/components/HomeCard/HomeCard.vue";
</script>
<template>
  <Hero/>
  <HomeCard/>
  <JobListings :limit="3" :show-button="true"/>
</template>