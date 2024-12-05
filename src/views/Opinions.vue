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
      console.log('Data received:', opinion);
      console.log(this.opinions);
 /*      this.opinions[0].author = 'test' */
      if (opinion.index !== undefined && opinion.updatedReview) {
      // Usar Vue.set para asegurar la reactividad
        this.$set(this.opinions, opinion.index, opinion.updatedReview);
      } else if (this.isEditing) {
        this.$set(this.opinions, this.editingIndex, opinion);
        this.isEditing = false;
      } else {
        this.opinions.push(opinion);
      }
      this.resetForm();
    },
/*       if (this.isEditing) {
        // Para cuando la llamada provenga del formulario normal
        this.opinions.splice(this.editingIndex, 1, opinion);
        this.isEditing = false;
      } else if (opinion.index !== undefined && opinion.updatedReview) {
        // Cuando la llamada provenga desde el Accordion con índice
        this.opinions.splice(opinion.index, 1, opinion.updatedReview);
      } else {
      // Agrega una nueva opinión
        this.opinions.push(opinion);
      }
      this.resetForm();
    }, */

    editOpinion(index) {
      this.newOpinion = { ...this.opinions[index] }; //load review data into the form
      this.isEditing = true;
      this.editingIndex = index;
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
/* .review-container {} */

h2 {
  margin: 2em;
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