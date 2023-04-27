<template>
    <div class="job-list">
        <div class="ordered-text">
            <p>Ordered by {{ order }}</p>
        </div>
        <transition-group name="list" tag="ul">
            <li v-for="job in OrderedJobs" :key="job.id">
                <h2>{{ job.title }} in {{ job.location }}</h2>
                <div class="salary">
                    <img src="@/assets/rupee.svg" alt="">
                    <p>
                        {{ job.salary }} Rupees
                    </p>
                </div>
                <div class="job-description">
                    <p>
                        Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore
                        et dolore magna aliqua.
                        Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
                        consequat.
                        Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla
                        pariatur.
                    </p>
                </div>
            </li>
        </transition-group>
    </div>
</template>
  
<script lang="ts">
import { defineComponent, PropType, computed } from 'vue'
import Job from '@/types/Job'
import OrderTerm from '@/types/OrderTerm'

export default defineComponent({
    props: {
        jobs: {
            required: true,
            type: Array as PropType<Job[]>
        },
        order: {
            required: true,
            type: String as PropType<OrderTerm>
        }
    },
    setup(props) {
        const OrderedJobs = computed(() => {
            return [...props.jobs].sort((a: Job, b: Job) => {
                return a[props.order] > b[props.order] ? 1 : -1
            })
        })

        return {OrderedJobs}
    }
})
</script>
  
<style scoped>
.job-list {
    max-width: 960px;
    margin: 40px auto;
}

.job-list ul {
    padding: 0;
}

.job-list li {
    list-style-type: none;
    background: white;
    padding: 16px;
    margin: 16px 0;
    border-radius: 4px;
}

.job-list h2 {
    margin: 0 0 10px;
    text-transform: capitalize;
}

.salary {
    display: flex;
}

.salary img {
    width: 30px;
}

.salary p {
    color: #17bf66;
    font-weight: bold;
    margin: 10px 4px;
}

.ordered-text {
    display: flex;
    justify-content: start;
}

.list-move{
    transition: all 1s;
}
</style>
  