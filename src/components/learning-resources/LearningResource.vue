<template>
  <li>
    <base-card>
      <header>
        <h3>{{ title }}</h3>
        <base-button mode="flat" @click="deleteResource(id)">Delete</base-button>
      </header>
      <p>{{ describtion }}</p>
      <nav>
        <a :href="link">Let's Go.</a>
      </nav>
    </base-card>
  </li>
</template>

<script>
// import BaseCard from '../ui/BaseCard.vue';
export default {
  components: {
    // 'base-card': BaseCard,
  },
  props: ['id', 'title', 'describtion', 'link'],
  inject:['deleteResource']
  // methods:{
  //   deleteResource(){

  //   }
  // }
};
</script>

<style scoped>
li {
  margin: auto;
  max-width: 40rem;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

h3 {
  font-size: 1.25rem;
  margin: 0.5rem 0;
}

p {
  margin: 0.5rem 0;
}

a {
  text-decoration: none;
  color: #ce5c00;
}

a:hover,
a:active {
  color: #c89300;
}
</style>