<template>
    <div>
        <div>
            <b-button v-b-modal.modal-prevent-closing variant="primary">Agregar</b-button>

        </div>
        <b-table striped hover :items="cursos" :fields="fields">
            <template v-slot:cell(actions)="row">
                <b-button v-b-modal.modal-prevent-closing @click="editarcurso(row.item)" variant="primary">Editar</b-button>
                <b-button @click="deletecurso(row.index)" variant="primary">Eliminar</b-button>
            </template>
        </b-table>
        <div>
            <b-modal id="modal-prevent-closing" ref="modal" title="Submit Your Name" @show="resetModal" @hidden="resetModal"
                @ok="handleOk">
                <form ref="form" @submit.stop.prevent="handleSubmit">
                    <b-form-group label="Nombre" label-for="name-input" invalid-feedback="Name is required"
                        :state="nameState">
                        <b-form-input id="nombre" v-model="cursoEdit.nombre" :state="nameState" required></b-form-input>
                    </b-form-group>
                    <b-form-group label="Url de la imagen" label-for="name-input" invalid-feedback="Name is required"
                        :state="nameState">
                        <b-form-input id="img" v-model="cursoEdit.img" :state="nameState" required></b-form-input>
                    </b-form-group>
                    <b-form-group label="cupos del curso" label-for="name-input" invalid-feedback="Name is required"
                        :state="nameState">
                        <b-form-input id="cupos" v-model="cursoEdit.cupos" :state="nameState" required></b-form-input>
                    </b-form-group>
                    <b-form-group label="inscritos del curso" label-for="name-input" invalid-feedback="Name is required"
                        :state="nameState">
                        <b-form-input id="inscritos" v-model="cursoEdit.inscritos" :state="nameState"
                            required></b-form-input>
                    </b-form-group>
                    <b-form-group label="Duracion del Curso" label-for="name-input" invalid-feedback="Name is required"
                        :state="nameState">
                        <b-form-input id="duracion" v-model="cursoEdit.duracion" :state="nameState" required></b-form-input>
                    </b-form-group>
                    <b-form-group label="Fecha de registro" label-for="name-input" invalid-feedback="Name is required"
                        :state="nameState">
                        <b-form-input id="nafecha_registrome-input" v-model="cursoEdit.fecha_registro" :state="nameState"
                            required></b-form-input>
                    </b-form-group>
                    <b-form-group label="Terminado" label-for="name-input" invalid-feedback="Name is required"
                        :state="nameState">
                        <b-form-input id="completado" v-model="cursoEdit.completado" :state="nameState"
                            required></b-form-input>
                    </b-form-group>
                    <b-form-group label="Costo del Curso" label-for="name-input" invalid-feedback="Name is required"
                        :state="nameState">
                        <b-form-input id="costo" v-model="cursoEdit.costo" :state="nameState" required></b-form-input>
                    </b-form-group>
                    <b-form-textarea id="textarea-small" v-model="cursoEdit.descripcion" size="sm"
                        placeholder="Comentario de actualizacion"></b-form-textarea>
                </form>
            </b-modal>
        </div>
        <div>
            <b-alert show variant="custom" class="alert-outline" style="border: solid 1px; color: blueviolet;"><i
                    class="fas fa-users" style="color: #882da9;"></i> Cantidad de Alumnos permitidos: {{ alumnosPermitidos
                    }} alumnos</b-alert>
            <b-alert show variant="custom" class="alert-outline" style="border: solid 1px; color: rgb(84, 158, 218);"><i
                    class="fas fa-user-plus" style="color: #548ef2;"></i> Cantidad de Alumnos Inscritos: {{ alumnosInscritos
                    }} alumnos</b-alert>
            <b-alert show variant="custom" class="alert-outline" style="border: solid 1px; color: rgb(235, 54, 54);"><i
                    class="fas fa-user-check" style="color: #e45874;"></i> Cantidad Total de cupos restantes: {{
                        cuposRestantes }} alumnos</b-alert>
            <b-alert show variant="custom" class="alert-outline" style="border: solid 1px; color: rgb(188, 136, 237);"><i
                    class="fas fa-ban" style="color: #3a0863;"></i> Cantidad total de cursos terminados:{{ cursosTerminados
                    }} cursos</b-alert>
            <b-alert show variant="custom" class="alert-outline" style="border: solid 1px; color: rgb(49, 73, 28);"><i
                    class="fas fa-bell" style="color: #44611a;"></i> Cantidad total de cursos activos: {{ cursosActivos }}
                cursos</b-alert>
            <b-alert show variant="custom" class="alert-outline" style="border: solid 1px; color: rgb(243, 84, 26);"><i
                    class="fas fa-bell" style="color: #f57914;"></i> Cantidad de cursos: {{ totalCursos }} cursos</b-alert>
        </div>
    </div>
</template>

<script>
import { mapState, mapGetters } from 'vuex';
export default {
    name: 'administracion-com',
    data: function () {
        return {
            cursoEdit: {},
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
        ...mapGetters(['alumnosPermitidos']),
        ...mapGetters(['alumnosInscritos']),
        ...mapGetters(['cursosTerminados']),
        ...mapGetters(['totalCursos']),
        cuposRestantes() {
            return this.alumnosPermitidos - this.alumnosInscritos
        },
        cursosActivos() {
            return this.totalCursos - this.cursosTerminados
        },
    },



    created() {

    },

    methods: {
        deletecurso(id) {
            console.log(id)
            this.cursos.splice(id, 1)
        },

        editarcurso(item) {
            console.log(item)
            this.cursoEdit = item
        },
        // agregarcurso() {
        //     this.cursos.push()
        // },

    },
}
</script>

<style scoped></style>
