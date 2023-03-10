<template>
  <div class="app">
    <header>
      <div class="order">
        <button @click="handleClick('title')">order by title</button>
        <button @click="handleClick('salary')">order by salary</button>
        <button @click="handleClick('location')">order by location</button>
      </div>
    </header>
    <JobList :jobs="jobs" :order="orderTerm" />
  </div>
</template>

<script lang="ts">
import JobList from "@/components/JobsList.vue";
import type { Job } from "@/types/Job";
import type { OrderTerm } from "@/types/OrderTerm";
import { defineComponent, ref } from "vue";

export default defineComponent({
  name: "App",
  components: {
    JobList,
  },
  setup() {
    const jobs = ref<Job[]>([
      {
        id: "1",
        title: "Farm worker",
        location: "Lon lon ranch",
        salary: 30000,
      },
      {
        id: "2",
        title: "Quarryman",
        location: "Death mountain",
        salary: 40000,
      },
      {
        id: "3",
        title: "Flute player",
        location: "The lost woods",
        salary: 35000,
      },
      { id: "4", title: "Fisherman", location: "Lake hylia", salary: 21000 },
      {
        id: "5",
        title: "Prison Guard",
        location: "Gerudo valley",
        salary: 32000,
      },
    ]);

    const orderTerm = ref<OrderTerm>("title");

    const handleClick = (term: OrderTerm): void => {
      orderTerm.value = term;
    };

    return { handleClick, jobs, orderTerm };
  },
  methods: {},
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
</style>
