<script setup>
// import jobData from "@/jobs.json";
import { ref, reactive, defineProps, onMounted } from "vue";
import JobListing from "@/components/JobListing.vue";
import { RouterLink } from "vue-router";
import axios from "axios";
import PulseLoader from "vue-spinner/src/PulseLoader.vue";

// const jobs = ref(jobData);
// const jobs = ref([]); 
const state = reactive({
  jobs: [],
  isLoading: true,
});

defineProps({
  limit: Number,
  showbutton: {
    type: Boolean,
    default: false,
  },
});

onMounted(async ()=>{
  try{

    const response = await axios.get('/apijobs');
    // jobs.value = respons.data;
    state.jobs = response.data;

  }catch (e){
    console.log(e)
  } finally {
    state.isLoading = false;
  }
})



</script>

<template>
  <section class="bg-blue-50 px-4 py-10">
    <div class="container-xl lg:container m-auto">
      <h2 class="text-3xl font-bold text-green-500 mb-6 text-center">
        Browse Jobs
      </h2>

      <!-- Show spinner -->
      <div v-if="state.isLoading" class="text-center text-gray-500 py-6"><PulseLoader/> </div>


      <!-- Show jobs lisitng -->
      <div v-else class="grid grid-cols-1 gap-6 md:grid-cols-3">
        <JobListing
          v-for="job in state.jobs.slice(0, limit || state.jobs.length)"
          :key="job.id"
          :job="job"
        />
      </div>
    </div>
  </section>

  <section v-if="showbutton" class="m-auto max-w-lg my-10 px-6">
    <RouterLink
      to="/jobs"
      class="block bg-black text-white text-center py-4 px-6 rounded-xl hover:bg-gray-700"
      >View All Jobs</RouterLink
    >
  </section>
</template>
