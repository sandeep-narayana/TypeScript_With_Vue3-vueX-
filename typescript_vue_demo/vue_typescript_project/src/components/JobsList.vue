<template>
  <div>
    <h1 class="title">Job Listings</h1>
    <div class="job_list">
      Ordered by {{ order }}
      <transition-group name="list" tag="ul">
        <li v-for="job in orderedJobs" :key="job.id" class="job_item">
          <h2 class="job_title">{{ job.title }} in {{ job.location }}</h2>
          <div class="salary">
            <p class="salary_amount">{{ job.salary }} rupees</p>
          </div>
          <div class="description">
            <p class="job_description">
              Lorem ipsum dolor sit amet consectetur adipisicing elit. Error
              dolorem quaerat, consequuntur, earum officiis cupiditate itaque
              aliquam in ipsam ea inventore! Tempore modi nihil perspiciatis
              saepe nemo tempora delectus? Aliquam!
            </p>
          </div>
        </li>
      </transition-group>
    </div>
  </div>
</template>

<script lang="ts">
import Job from "@/types/job";
import OrderTerm from "@/types/OrderTerm";
import { computed, defineComponent, PropType } from "vue";

export default defineComponent({
  name: "JobsList",
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
      return [...props.jobs].sort((a: Job, b: Job) => {
        return a[props.order] > b[props.order] ? 1 : -1;
      });
    });
    return { orderedJobs };
  },
});
</script>

<style scoped>
.title {
  font-size: 24px;
  margin-bottom: 20px;
}

.job_list {
  border: 1px solid #ccc;
  padding: 20px;
  border-radius: 5px;
  background-color: #f7f7f7;
}

.job_item {
  margin: 20px 0;
  padding: 20px;
  background-color: #fff;
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
  border-radius: 5px;
}

.job_title {
  font-size: 20px;
  color: #333;
}

.salary_amount {
  font-weight: bold;
  margin-top: 10px;
}

.job_description {
  font-size: 14px;
  color: #666;
}

.list-move {
  transition: all 1s;
}
</style>
