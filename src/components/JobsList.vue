<template>
  <div class="job-list">
    <p>Ordered by {{ order }}</p>
    <ul>
      <li :key="job.id" v-for="job in orderedJobs">
        <h2>{{ job.title }} in {{ job.location }}</h2>
        <div class="salary">
          <p>{{ job.salary }}</p>
        </div>
        <div class="description">
          <p>
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Dolore
            obcaecati sunt maiores nesciunt, molestias modi atque rerum aliquid
            laudantium distinctio, cupiditate sed veniam ab animi eveniet soluta
            ullam recusandae molestiae?
          </p>
        </div>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import { Job } from "@/types/Job";
import { type OrderTerm } from "@/types/OrderTerm";
import { computed, defineComponent, PropType } from "vue";

export default defineComponent({
  props: {
    jobs: {
      required: true,
      type: Array as PropType<Job[]>,
    },
    order: {
      required: true,
      type: String as PropType<OrderTerm>,
    },
  },
  setup(props) {
    const orderedJobs = computed(() => {
      return [...props.jobs].sort((a, b) => {
        return a[props.order] > b[props.order] ? 1 : -1;
      });
    });
    return { orderedJobs };
  },
});
</script>

<style>
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
</style>
