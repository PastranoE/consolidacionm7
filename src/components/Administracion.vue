<template>
    <div>
        <b-table striped hover :items="cursos" :fields="fields">
            <template v-slot:cell(actions)="row">
                <b-button @click="verList(row.item)" variant="primary">Editar</b-button>
                <b-button @click="deletecurso(row.index)" variant="primary">Eliminar</b-button>
            </template>
        </b-table>
    </div>
</template>

<script>
import { mapState } from 'vuex';
export default {
    name: 'administracion-com',
    data: function () {
        return {
            fields: [
                { key: 'nombre', label: 'Curso' },
                { key: 'cupos', label: 'Cupos' },
                { key: 'inscritos', label: 'Inscritos' },
                { key: 'costo', label: 'Costo' },
                { key: 'completado', label: 'terminado' },
                { key: 'fecha_registro', label: 'fecha' },
                { key: 'actions', label: 'Acciones' }
            ]
            //     {
            //     "id": 1,
            //     "img": "https://i.blogs.es/545cf8/es6-logo/450_1000.png",
            //     "nombre": "JavaScript Avanzado",
            //     "costo": 30000,
            //     "duracion": "2 meses",
            //     "cupos": 20,
            //     "inscritos": 10,
            //     "completado": false,
            //     "fecha_registro": "06/03/2022",
            //     "descripcion": "Curso con las nuevas actualizaciones de JavaScript."
            //   }
        }
    },
    computed: {
        ...mapState(['cursos']),

    },



    created() {

    },

    methods: {
        deletecurso(id) {
            console.log(id)
            this.cursos.splice(id, 1)
        }
    },
}
</script>

<style scoped></style>
