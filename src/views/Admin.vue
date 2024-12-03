<template>
  <div>
    <h1>Panel de Administración</h1>
    <p>Nombre: {{ user.firstName }}</p>
    <p>Apellido: {{ user.lastName }}</p>
  </div>
</template>

<script>
export default {
    name: 'component-name',
    // props: {},
    data() {
        return {
            user: { // sólo un ejemplo
                firstName: 'Juan',
                lastName: 'Pérez',
            },
        };
    },
    // computed: {},
    //methods: {}
    // watch: {},
    // components: {},
    // mixins: [],
    // filters: {},
    // -- Lifecycle Methods
    // -- End Lifecycle Methods
};
</script>

<style scoped>
    
</style>