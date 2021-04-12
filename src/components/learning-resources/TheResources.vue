<template>
  <base-card>
    <base-button
      @click="setSelectedTab('resource-box')"
      :mode="resourceBoxMode"
    >
      Resource Box
    </base-button>
    <base-button
      @click="setSelectedTab('add-resource')"
      :mode="addResourceMode"
    >
      Add Resource
    </base-button>
  </base-card>
  <keep-alive>
    <component
      :is="selectedTab"
      :submit-new-resource="addNewResource"
    ></component
  ></keep-alive>
</template>

<script>
import ResourceBox from './ResourceBox.vue';
import AddResource from './AddResource.vue';

export default {
  components: {
    ResourceBox,
    AddResource,
  },
  provide() {
    return {
      resourceData: this.resourceData,
      addNewResource: this.addNewResource,
      deleteResource: this.deleteResource,
    };
  },
  data() {
    return {
      selectedTab: 'resource-box',
      resourceData: [
        {
          id: 'google-page',
          title: 'Google page',
          describtion: 'How you can learn the most knowlege in the earth.',
          link: 'https://google.com',
        },
        {
          id: 'vue-page',
          title: 'Vue page',
          describtion: 'How you can learn the Vue.js.',
          link: 'https://vuejs.org/v2/guide/instance.html',
        },
      ],
    };
  },
  computed: {
    resourceBoxMode() {
      return this.selectedTab === 'resource-box' ? null : 'flat';
    },
    addResourceMode() {
      return this.selectedTab === 'add-resource' ? null : 'flat';
    },
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    },
    addNewResource(title, describtion, link) {
      console.log(title, describtion, link);
      const newResource = {
        id: new Date().toISOString(),
        title: title,
        describtion: describtion,
        link: link,
      };
      this.resourceData.unshift(newResource);
      this.setSelectedTab('resource-box');
    },
    deleteResource(id) {
      const index = this.resourceData.findIndex((data) => data.id === id);
      this.resourceData.splice(index, 1);
    },
  },
};
</script>