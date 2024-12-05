<template>
  <div>
    <div v-for="(review, index) in reviews" :key="index" class="accordion">
      <div class="accordion-header" @click="toggleAccordion(index)">
        <p>Review made by: <strong>{{ review.author }}</strong></p>
        <button class="toggle-button">{{ openIndex === index ? 'Hide' : 'Show' }} Details</button>
      </div>

      <div v-if="openIndex === index" class="accordion-body">
        <p>Review: {{ review.text }}</p>
        <div class="actions">
          <button class="edition" @click="startEditing(index, review)" aria-label="Edit review">Edit</button>
          <button class="deletion" @click="deleteOpinion(index)" aria-label="Delete review">Delete</button>
        </div>

        <!-- Render the OpinionForm when editing -->
        <OpinionForm 
          v-if="editingIndex === index" 
          :newOpinion="reviewToEdit"
          :isEditing="true"
          @sendOpi="saveEdit(index)"
        />
      </div>
    </div>
  </div>
</template>

<script>
import OpinionForm from './OpinionForm.vue';

export default {
  name: 'OpinionAccordion',
  props: ['reviews'],
  components: { OpinionForm },
  data() {
    return {
      openIndex: null,        // Tracks which accordion is open
      editingIndex: null,     // Tracks which review is being edited
      reviewToEdit: null,     // Holds the review data for editing
    };
  },
  methods: {
    toggleAccordion(index) {
      this.openIndex = this.openIndex === index ? null : index;
    },
    startEditing(index, review) {
      this.editingIndex = index;  //set the index for editing
      this.reviewToEdit = { ...review };  //pass a copy of the review to the form
    },
    saveEdit(index) {
      console.log('Save Edit triggered:', index, this.reviewToEdit);
      this.$emit('update', { index, updatedReview: this.reviewToEdit });  //emitir el índice y la opinión actualizada
      this.editingIndex = null;  //cerrar la edición
    },
    deleteOpinion(index) {
      this.$emit('delete', index);  //pass the index to the parent for deletion
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
.edition {
  margin-right: 0.5em;
  padding: 0.5em 1em;
  border: none;
  cursor: pointer;
  background-color: #007bff;
  color: white;
  border-radius: 3px;
}
.edition:hover {
  background-color: #0056b3;
}

.deletion {
  background-color: #ff4d4d;
  color: white;
  border-radius: 3px;
  margin-right: 0.5em;
  padding: 0.5em 1em;
  border: none;
  cursor: pointer;
}
.deletion:hover {
  background-color: #ff3333;
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