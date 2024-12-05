<template>
  <!-- este form manejará la creación y actualización de opiniones -->
  <form @submit.prevent="addOrUpdateOpinion">
    <label for="author">Name:</label>
    <input id="author" v-model="localOpinion.author" placeholder="Enter your name or alias" required />
    <label for="review">Review:</label>
    <textarea id="review" v-model="localOpinion.text" rows="6" placeholder="Write your review here..." required></textarea>

    <button type="submit">{{ isEditing ? 'Update' : 'Add' }} Review</button>
  </form>
</template>

<script>
export default {
  name: 'form-component',
  props: {
    newOpinion: Object,
    isEditing: Boolean,
  },
  data() {
    return {
      localOpinion: { ...this.newOpinion },  // Create local copy for form editing
    };
  },
  watch: {
    newOpinion: {
      immediate: true, // Asegura que se ejecuta al montar el componente
      handler(newVal) {
        this.localOpinion = { ...newVal };  // Update local data when newOpinion changes
      },
      deep: true  // Observa cambios profundos en el objeto
    }
  },
  methods: {
    addOrUpdateOpinion() {
      console.log('Sending opinion:', this.localOpinion)
      this.$emit('sendOpi', { ...this.localOpinion });  // Emit form data to parent
      this.localOpinion = { author: '', text: '' };  // Reset form
    }
  }
};
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  gap: 1em;
}
input, textarea {
  padding: 0.5em;
  border: 1px solid #ccc;
}
button {
  align-self: flex-start;
  margin-right: 0.5em;
}  
</style>