<template>
  <div class="app">
    <!-- <h2 class="hero">
      Hello, Manmansui
    </h2> -->
    <div class="title">
      <img src="./assets/heart.svg" alt="">
      <h1>Witchcraft Jobs</h1>
    </div>
    <div class="sort-button">
      <button @click="handleClick('title')">order by title</button>
      <button @click="handleClick('salary')">order by salary</button>
      <button @click="handleClick('location')">order by location</button>
    </div>

    <JobList :jobs="jobs" :order="order" />


  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, ref, toRefs } from 'vue';
import JobList from './components/JobList.vue'
import Job from './types/Job'
import OrderTerm from './types/OrderTerm'


export default defineComponent({
  name: 'App',
  components: { JobList },
  setup() {
    const jobs = ref<Job[]>([
      { title: 'Architect', location: 'Kota Kinabalu', salary: 10000, id: '1' },
      { title: 'quarryman', location: 'death mountain', salary: 40000, id: '2' },
      { title: 'Witches', location: 'the lost woods', salary: 35000, id: '3' },
      { title: 'fisherman', location: 'lake hylia', salary: 21000, id: '4' },
      { title: 'prison guard', location: 'gerudo valley', salary: 32000, id: '5' }
    ])

    const order = ref<OrderTerm>('title')

    const handleClick = (term: OrderTerm) => {
      order.value = term
    }

    return { jobs, handleClick, order }
  }
});
</script>

<style>
header {
  text-align: center;
}

header .order {
  margin-top: 20px;
}

button {
  margin: 0 10px;
  color: #1195c9;
  border: 3px solid #1195c9;
  background: #d5f0ff;
  padding: 8px 16px;
  border-radius: 4px;
  cursor: pointer;
  font-weight: bold;
}

.sort-button {
  display: flex;
  justify-content: center;
}

.title {
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
  margin-top: 30px;
}

.title img {
  width: 60px;
  margin-right: 20px;
}

.title h1 {
  font-size: 3em;
}</style>
