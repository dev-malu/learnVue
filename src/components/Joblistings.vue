<script setup lang="ts">
import Joblisting from '@/components/Joblisting.vue';
import { reactive, defineProps, onMounted } from 'vue';
import { RouterLink } from 'vue-router';
import axios from 'axios';

type LimitProps = {
  limit: number,
  showButton: {
    type: boolean,
    default: false
  }
};


const props = defineProps<LimitProps>();
const state = reactive({
  jobs: [],
  isLoading: true
});

onMounted(async () => {
  try {
    const res = await axios.get('/api/jobs');
    state.jobs = res.data;
  } catch (error) {
    console.log('Error:', error);
  } finally {
    state.isLoading = false;
  }
});
</script>

<template>
  <!-- Browse Jobs -->
  <section class="bg-green-50 px-4 py-10">
    <div class="container-xl lg:container m-auto">
      <h2 class="text-3xl font-bold text-green-500 mb-6 text-center">
        Browse Jobs
      </h2>
      <!-- Job Listing 1 -->
      <div class="grid grid-cols-1 gap-6 md:grid-cols-3">
        <Joblisting v-for="item in state.jobs.slice(0, props.limit) || state.jobs.length" :key="item.id" :job="item" />
      </div>
    </div>
  </section>
  <section v-if="props.showButton" class="m-auto max-w-lg my-10 px-6">
    <RouterLink to="/jobs" class="block bg-black text-white text-center py-4 px-6 rounded-xl hover:bg-gray-700">View All
      Jobs</RouterLink>
  </section>
</template>
