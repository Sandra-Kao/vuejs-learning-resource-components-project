<template>

  <base-dialog v-if="!isInputValidated" title="Invalid Input" @close="confirmDailog">
    <teloprot to="body">
      <template #default><p>This is a Invalid Input, please reentry again.</p></template>
      <template #action><base-button @click="confirmDailog">Okay</base-button></template>
    </teloprot>
  </base-dialog>

  <base-card>
    <form @submit.prevent="submitNewResource">
      <div class="form-control">
        <label for="title">Title</label>
        <input id="title" name="title" type="text" ref="titleInput" />
      </div>
      <div class="form-control">
        <label for="description">Description</label>
        <textarea
          id="description"
          name="description"
          rows="3"
          ref="descriptionTextarea"
        />
      </div>
      <div class="form-control">
        <label for="link">Link</label>
        <input id="link" name="link" type="url" ref="linkInput" />
      </div>
      <div>
        <base-button type="submit">Add Resource</base-button>
      </div>
    </form>
  </base-card>
</template>

<script>
import BaseButton from '../ui/BaseButton.vue';
import BaseCard from '../ui/BaseCard.vue';
import BaseDialog from '../ui/BaseDialog.vue';
export default {
  inject: ['addNewResource'],
  components: { BaseCard, BaseButton, BaseDialog },
  data() {
    return {
      isInputValidated: true,
    };
  },
  methods: {
    confirmDailog() {
      this.isInputValidated = true;
    },
    submitNewResource() {
      const titleInput = this.$refs.titleInput.value;
      const descriptionTextarea = this.$refs.descriptionTextarea.value;
      const linkInput = this.$refs.linkInput.value;

      if (
        titleInput.trim() === '' ||
        descriptionTextarea.trim() === '' ||
        linkInput.trim() === ''
      ) {
        this.isInputValidated = false;
        return;
      } else {
        this.isInputValidated = true;
        this.addNewResource(titleInput, descriptionTextarea, linkInput);
      }
    },
  },
};
</script>

<style scope>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>