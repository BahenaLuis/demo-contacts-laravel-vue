<template>
    <div class="container">
        <button
            type="button"
            class="btn btn-primary"
            v-on:click="showModalCreate"
        >
            New
        </button>

        <div class="row">
            <div class="col">
                <table class="table">
                    <thead>
                        <tr>
                            <th scope="col">#</th>
                            <th scope="col">Student Id</th>
                            <th scope="col">Firstname</th>
                            <th scope="col">Lastname</th>
                            <th scope="col">Email</th>
                            <th scope="col">Age</th>
                            <th scope="col">Edit</th>
                            <th scope="col">Remove</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="s in students" :key="s.id">
                            <td>{{ s.id }}</td>
                            <td>{{ s.student_id }}</td>
                            <td>{{ s.firstname }}</td>
                            <td>{{ s.lastname }}</td>
                            <td>{{ s.email }}</td>
                            <td>{{ s.age }}</td>
                            <td>
                                <button type="button" class="btn btn-link" v-on:click="showModalUpdate(s)">Edit</button>                                
                            </td>
                            <td>
                                <button type="button" class="btn btn-link" v-on:click="removeStudent(s)">Remove</button>                                
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>

        <create-student
            v-on:close-modal-create="closeModalCreate"
            v-if="modalCreateStudent"
        ></create-student>
        <div class="modal-backdrop fade show" v-if="modalCreateStudent"></div>  

        <!-- <component 
            :is="update-student" 
            v-on:close-modal-update="closeModalUpdate"
            v-if="modalUpdateStudent"
            v-bind:student="student"
        ></component> -->

        <update-student
            v-on:close-modal-update="closeModalUpdate"
            v-if="modalUpdateStudent"
            v-bind:student-values="student"
        ></update-student>
        <div class="modal-backdrop fade show" v-if="modalUpdateStudent"></div>  

    </div>
</template>

<script>
import CreateStudent from "./Modals/CreateStudent.vue";
import UpdateStudent from "./Modals/UpdateStudent.vue";
import { Link } from "@inertiajs/inertia-vue3";
export default {
    name: "index.note",

    //Components wich will be in this component
    components: {
        CreateStudent,
        UpdateStudent,
        Link,
    },

    //variables wich will be received
    props: {
        students: Array,
    },

    //variables wich are use in this component
    data() {
        return {
            titleModal: "",
            modalCreateStudent: false,
            modalUpdateStudent: false,
            student: Object,
        };
    },

    //functions wich will be executed in this component for differents elements or components
    methods: {
        showModalCreate() {            
            this.modalCreateStudent = true;
        },
        closeModalCreate() {        
            this.modalCreateStudent = false;
        },

        showModalUpdate(student) {            
            this.student = student;
            this.modalUpdateStudent = true;
        },
        closeModalUpdate() {            
            this.modalUpdateStudent = false;
        },
        removeStudent(student) {
            if(confirm("¿Quieres eliminar este registro?")) {
                this.$inertia.delete(this.route("students.destroy", student));
            }            
        }
    },

    //variables que cambian su valor dependiendo de otras variables
    computed: {},

    //variables that changed depending of the change of a variable
    //also in watch we can to perform operations complex like calls http or asyn calls
    watch: {},
};
</script>
