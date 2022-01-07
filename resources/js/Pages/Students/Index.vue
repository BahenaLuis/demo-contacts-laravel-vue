<template>
    <div class="container">

        <button v-on:click="showModalCreate" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">New</button>

        <table class="table-fixed">
            <thead>
                <tr>
                    <th>#</th>
                    <th>Student Id</th>
                    <th>Firstname</th>
                    <th>Lastname</th>
                    <th>Email</th>
                    <th>Age</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="s in students" :key="s.id">
                    <td>{{ s.id }}</td>
                    <td>{{ s.studentId }}</td>
                    <td>{{ s.firstname }}</td>
                    <td>{{ s.lastname }}</td>
                    <td>{{ s.email }}</td>
                    <td>{{ s.age }}</td>

                    <td>
                        <button v-on:click="showModalUpdate(s)">Edit</button>
                    </td>     
                    <td>
                        <Link :href="route('students.destroy', s)" method="delete">Remove</Link>
                    </td>

                </tr>
            </tbody>
        </table>

        <create-student 
            v-on:close-modal-create="closeModalCreate" 
            v-if="modalCreateStudent"            
        ></create-student>
        

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

    </div>
</template>

<script>
import CreateStudent from './Modals/CreateStudent.vue';
import UpdateStudent from './Modals/UpdateStudent.vue';
import { Link } from '@inertiajs/inertia-vue3'
export default {
    name: "index.note",

    //Components wich will be in this component
    components: {
        CreateStudent,
        UpdateStudent,
        Link
    },

    //variables wich will be received
    props: {
        students: Array,        
    },

    //variables wich are use in this component
    data() {
        return {
            titleModal: '',
            modalCreateStudent: false,
            modalUpdateStudent: false,
            student: Object
        };
    },

    //functions wich will be executed in this component for differents elements or components
    methods: {
        showModalCreate() {
            console.log("showModalCreate");
            this.modalCreateStudent = true;
        },
        closeModalCreate() {
            console.log("closeModalCreate");
            this.modalCreateStudent = false;
        },

        showModalUpdate(student) {            
            console.log("showModalUpdate");
            this.student = student;
            this.modalUpdateStudent = true;
        },
        closeModalUpdate() {
            console.log("closeModalUpdate");
            this.modalUpdateStudent = false;
        },
    },

    //variables that changed depending of other variables
    computed: {    
    },

    //variables that changed depending of the change of a variable
    //also in watch we can to perform operations complex like calls http or asyn calls
    watch: {        
    },
};
</script>
