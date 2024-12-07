<template>
  <div class="review-container">
    <h2>Leave your comment here about: {{ gameName }}</h2>
    <opinion-form :newOpinion="newOpinion" :isEditing="isEditing" @sendOpi="addOrUpdateOpinion" />
    <div class="reviews-container">
      <h2>You can see your comment below.</h2>
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
      //console.log('Data received:', opinion);
      this.opinions.push(opinion);
    },
    editOpinion(opinion) {
      this.isEditing = false;
      this.editingIndex = opinion.index;
      this.opinions.splice(opinion.index,1, opinion.updatedReview)
    },
    deleteOpinion(index) {
      this.opinions.splice(index, 1);
      this.isEditing = false; 
      this.resetForm(); 
    },
    resetForm() {
      this.newOpinion = { author: '', text: '' };
      this.editingIndex = null;
      this.isEditing = false;
    }
  },
  components: { OpinionForm, OpinionAccordion }, 
};
</script>

<style scoped>
h2 {
  margin: 2em;
}

.no-reviews {
  margin-top: 60px;  /* Push to bottom */
  margin: 2em;
  padding: 20px;
  background-color: #ffebeb;  /* Light red background */
  color: #d32f2f;  /* Darker red text */
  font-size: 1.5em;
  border: 1px solid #d32f2f;
  text-align: center;
  border-radius: 8px;
}
</style>