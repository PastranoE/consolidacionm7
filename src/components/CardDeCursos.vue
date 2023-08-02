<template>
<div>
    <v-row justify="space-around">
          <v-card width="400">
            <v-img height="200px" :src="curso.img">
              <v-app-bar flat color="rgba(0, 0, 0, 0)">
                <v-app-bar-nav-icon color="white"></v-app-bar-nav-icon>

                <v-toolbar-title class="text-h6 white--text pl-0">

                </v-toolbar-title>

                <v-spacer></v-spacer>

                <v-btn color="white" icon>
                  <v-icon>mdi-dots-vertical</v-icon>
                </v-btn>
              </v-app-bar>
            </v-img>

            <v-card-text>
              <div class="font-weight-bold ml-8 mb-2">
              {{ curso.nombre }}
              </div>

              <v-timeline align-top dense>

                <v-timeline-item small :color="colors[1]"
            >
                  <div>
                    <div class="font-weight-normal">
                      <strong>Costo: {{ curso.costo  }}</strong> 
                    </div>
                    <div> Duración: {{ curso.duracion }}</div>
                  </div>
                </v-timeline-item>
                <v-timeline-item small :color="colors[0]">
                  <div>
                    <div class="font-weight-normal">
                      <strong>Cupos: {{ curso.cupos  }}</strong>
                    </div>
                    <div>Completado: {{ curso.completado }}</div>
                  </div>
                </v-timeline-item>
                <v-timeline-item small :color="colors[1]">
                  <div>
                    <div class="font-weight-normal">
                      <strong>Fecha de Registro:</strong>
              
                    </div>
                    <div>{{ curso.fecha_registro}}</div>
                  </div>
                </v-timeline-item>
                <v-timeline-item small :color="colors[0]">
                  <div>
                    <div class="font-weight-normal">
                      <strong>Descripción:</strong> 
                    </div>
                    <div>{{ curso.descripcion }}</div>
                  </div>
                </v-timeline-item>
              </v-timeline>
            </v-card-text>
          </v-card>
        </v-row>
</div>
</template>

<script>
export default {
    name: 'carddecursos-comp',
    props: {
        curso:{
            type: Object,
            required: true
        }
    },
    data: function(){
        return {
            colors:['purple','green']
        }
    },
    // computed: {},
    //methods: {}
    // watch: {},
    // components: {},
    // mixins: [],
    // filters: {},
    // -- Lifecycle Methods
    // -- End Lifecycle Methods
}
</script>

<style scoped>
    
</style>