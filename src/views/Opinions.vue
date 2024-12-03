<template>
  <div>
    <h1>Reviews about: {{ gameName }}</h1>
    <opinion-form :newOpinion="newOpinion" :isEditing="isEditing" @submit="addOrUpdateOpinion" />
    <div class="reviews-container">
      <opinion-accordion :reviews="opinions" 
                       @edit="editOpinion" 
                       @delete="deleteOpinion" />
      <p v-if="opinions.length === 0" class="no-reviews">There are no reviews yet.</p>
    </div>
  </div>
</template>

<script>
import OpinionForm from '@/components/OpinionForm.vue';
import OpinionAccordion from '@/components/OpinionAccordion.vue';

export default {
  name: 'opinions-view',
  props: ['game'],
  data() {
    return {
      gameName: this.game,  //captura el parámetro de ruta dinámica
      opinions: [],  //array local para almacenar las opiniones del juego
      newOpinion: { author: '', text: '' }, //autor y texto de la opinión
      isEditing: false, //marcar para comprobar si el usuario está editando una opinión existente
      editingIndex: null, //índice de la opinión en proceso de edición
    };
  },
  methods: {
    addOrUpdateOpinion(opinion) {
      if (this.isEditing) {
        // Actualiza la opinión existente
        this.opinions.splice(this.editingIndex, 1, opinion);
        this.isEditing = false;
      } else {
        // Agrega una nueva opinión
        this.opinions.push(opinion);
      }
      this.newOpinion = { author: '', text: '' };  //resetear form
    },
    editOpinion(index) {
      this.newOpinion = { ...this.opinions[index] };
      this.isEditing = true;
      this.editingIndex = index;
    },
    deleteOpinion(index) {
      this.opinions.splice(index, 1);
      this.isEditing = false; 
      this.newOpinion = { author: '', text: '' };  
    },
  },
  components: { OpinionForm, OpinionAccordion }, 
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
.opinion {
  border: 1px solid #ddd;
  padding: 1em;
  margin-bottom: 1em;
}

.no-reviews {
  margin-top: 60px;  /* Push to bottom */
  padding: 20px;
  background-color: #ffebeb;  /* Light red background */
  color: #d32f2f;  /* Darker red text */
  font-size: 1.5em;
  border: 1px solid #d32f2f;
  text-align: center;
  border-radius: 8px;
}
</style>