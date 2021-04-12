<template>
  <ul>
    <learning-resource
      v-for="data in resourceData"
      :key="data.id"
      :id="data.id"
      :title="data.title"
      :describtion="data.describtion"
      :link="data.link"
    ></learning-resource>
  </ul>
</template>

<script>
import LearningResource from './LearningResource.vue';
export default {
  components: {
    LearningResource
  },
  inject: ['resourceData']
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
  margin: auto;
  max-width: 40rem;
}
</style>