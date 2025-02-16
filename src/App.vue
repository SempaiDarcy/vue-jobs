<script setup>
import Navbar from "@/components/Navbar/Navbar.vue";
import Hero from "@/components/Hero/Hero.vue";
import HomeCard from "@/components/HomeCard/HomeCard.vue";
import JobListings from "@/components/JobListings/JobListings.vue";
</script>
<template>
  <Navbar/>
  <Hero title="Test title" subTitle="Test subtitle"/>
  <HomeCard/>
  <JobListings :limit="3" :show-button="true"/>
</template>