<template>
  <CollectionsList
    :jobs="getJobsData"
    @slideout="openSidebar"
  />
  <div v-if="slideout" :key="render">
    <CollectionsAdd @postBody="postData" />
  </div>
</template>
<script setup lang="ts">
const slideout = ref(false);
const render = ref(0);
//GET Call
const getOptions = {
  method: "GET",
  headers: {
    "Content-Type": "application/json",
    Authorization: `Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1IjoiYzNlZTRlOWU1NTk2NDdjZDk4NGVmMzFhNjc4ODNkMmEiLCJkIjoiMTY4MDEwOCIsInIiOiJzYSIsInAiOiJmcmVlIiwiYSI6ImZpbmRlci5pbyIsImwiOiJ1czEiLCJleHAiOjE2ODMzNDkzOTB9.0V2YBlGbEMRMwE5sh1m-7WqAqfbB4_Fmqy9PX5rQoRo`,
  },
};
let getData = useAuthLazyFetch(
  "https://v7-stark-db-orm.mercury.infinity-api.net/api/jobs/?offset=0&limit=100&sort_column=id&sort_direction=desc",
  getOptions
);
let getJobsData = ref(getData.data._rawValue);
//POST Call to send Data to the list
const postData = async (body: Object) => {
  const options = {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1IjoiYzNlZTRlOWU1NTk2NDdjZDk4NGVmMzFhNjc4ODNkMmEiLCJkIjoiMTY4MDEwOCIsInIiOiJzYSIsInAiOiJmcmVlIiwiYSI6ImZpbmRlci5pbyIsImwiOiJ1czEiLCJleHAiOjE2ODMzNDkzOTB9.0V2YBlGbEMRMwE5sh1m-7WqAqfbB4_Fmqy9PX5rQoRo`,
    },
    body: JSON.stringify(body),
  };
    useAuthLazyFetchPost(
    "https://v7-stark-db-orm.mercury.infinity-api.net/api/jobs/",
    options
  );
  //for showing the recent data first
  getJobsData.value.unshift(body);
  
  slideout.value = false;
};
const openSidebar = () => {
  slideout.value = true;
  render.value++;
};
</script>
