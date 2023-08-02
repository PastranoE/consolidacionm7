<template>
  <div>
    <div class="container">
      <h3>Lista de Cursos</h3>


      <v-container >
        <v-row>
        <v-col cols="12" md="4" lg="4" v-for="curso in cursos" :key="curso.id">
          <CardDeCursos :curso="curso"/>
        </v-col>
      </v-row>
      
      </v-container>

    </div>

  </div>
</template>

<script>
import { mapState } from 'vuex';

import CardDeCursos from '@/components/CardDeCursos.vue';
export default {
  components: { CardDeCursos },
  name: 'Home-view',
  // props: ['course'],
  data: function () {


    return {
    
    }
  },
  created() {
    this.messages;
  },
  computed: {
    ...mapState(['cursos'])
  },
  //methods: {}
  // watch: {},
  // components: {},
  // mixins: [],
  // filters: {},
  // -- Lifecycle Methods
  // -- End Lifecycle Methods
}

</script>

<style scoped></style> 