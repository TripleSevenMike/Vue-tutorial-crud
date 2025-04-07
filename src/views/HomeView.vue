
<script setup>

import Hero from "@/components/Hero.vue";
import HomeCards from "@/components/HomeCards.vue";
import JobsListings from "@/components/JobListings.vue";
</script>
  

<template>
  <Hero
    title="Become a Vue Dev"
    subTitle="Find the Vue job that fits your skills and needs"
    />
  <HomeCards />
  <JobsListings
    :limit="3"
    :showbutton="true"/>
</template>
