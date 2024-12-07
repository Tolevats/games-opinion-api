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
          @sendOpi="saveEdit($event,index)"
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
      openIndex: null, //tracks which accordion is open
      editingIndex: null, //tracks which review is being edited
      reviewToEdit: null, //holds the review data for editing
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
    saveEdit(event,index) {
      //console.log('Save Edit triggered:', index, event);
      this.$emit('edit', { index, updatedReview: event });
      this.editingIndex = null;
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
  margin: 2em;
  overflow: hidden;
}
.accordion-header {
  color: #333;
  background-color: #f1f1f1;
  padding: 1em;
  cursor: pointer;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.accordion-body {
  padding: 1em;
  color: #333;
  background-color: #fafafa;
}
.actions {
  margin-top: 1em;
}

.edition, .deletion {
  color: white;
  font-size: 1em;
  margin: 0.8em 1.5em 0 0;
  padding: 0.8em 1.5em;
  border: none;
  border-radius: 8px;
  cursor: pointer;

}
.edition {
  background-color: #007bff;
}
.edition:hover {
  background-color: #0056b3;
}

.deletion {
  background-color: #ff4d4d;
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