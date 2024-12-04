<template>
  <div>
    <div v-for="(review, index) in reviews" :key="index" class="accordion">
      <div class="accordion-header" @click="toggleAccordion">
        <strong>{{ review.author }}</strong>
        <button class="toggle-button">{{ isOpen ? 'Hide' : 'Show' }} Details</button>
      </div>

      <div v-if="isOpen" class="accordion-body">
        <p>{{ review.text }}</p>
        <div class="actions">
          <button @click="editOpinion" aria-label="Edit review">Edit</button>
          <button @click="deleteOpinion" aria-label="Delete review">Delete</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'OpinionAccordion',
  props: ['reviews'],
  data() {
    return {
      isOpen: false, // Controls accordion visibility
    };
  },
  methods: {
    toggleAccordion() {
      this.isOpen = !this.isOpen; // Toggle visibility
    },
    editOpinion() {
      this.$emit('edit', this.opinion); // Pass opinion data
    },
    deleteOpinion() {
      this.$emit('delete', this.opinion); // Pass opinion data
    },
  },
};
</script>

<style scoped>
.accordion {
  border: 1px solid #ccc;
  border-radius: 5px;
  margin-bottom: 1em;
  overflow: hidden;
}
.accordion-header {
  background-color: #f1f1f1;
  padding: 1em;
  cursor: pointer;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.accordion-body {
  padding: 1em;
  background-color: #fafafa;
}
.actions {
  margin-top: 1em;
}
button {
  margin-right: 0.5em;
  padding: 0.5em 1em;
  border: none;
  cursor: pointer;
  background-color: #007bff;
  color: white;
  border-radius: 3px;
}
button:hover {
  background-color: #0056b3;
}
.toggle-button {
  background: none;
  color: #007bff;
  border: none;
  cursor: pointer;
}
.toggle-button:hover {
  text-decoration: underline;
}
</style>