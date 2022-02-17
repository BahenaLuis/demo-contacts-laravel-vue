<template>
    <div
        class="modal fade show"
        id="modalCreate"
        tabindex="-1"
        role="dialog"
        aria-labelledby="exampleModalLabel"
        style="display: block; padding-right: 17px"
        aria-modal="true"
    >
        <div class="modal-dialog" role="document">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title" id="exampleModalLabel">
                        New student
                    </h5>
                </div>
                <div class="modal-body">
                    
                    <!-- Validation of errors -->
                    <div v-if="validationErrors">
                        <ul class="alert alert-danger">
                            <li
                                v-for="(value, key, index) in validationErrors"
                                :key="index"
                            >
                                {{ value }}
                            </li>
                        </ul>
                    </div>

                    <form @submit.prevent="createStudent">
                        <div class="form-group">
                            <label for="firstname">Firstname</label>
                            <input
                                type="text"
                                class="form-control"
                                id="firstname"
                                v-model="form.student.firstname"
                            />
                        </div>
                        <div class="form-group">
                            <label for="lastname">Lastname</label>
                            <input
                                type="text"
                                class="form-control"
                                id="lastname"
                                v-model="form.student.lastname"
                            />
                        </div>
                        <div class="form-group">
                            <label for="email">Email</label>
                            <input
                                type="email"
                                class="form-control"
                                id="email"
                                aria-describedby="emailHelp"
                                v-model="form.student.email"
                            />
                        </div>
                        <div class="form-group">
                            <label for="age">Age</label>
                            <input
                                type="text"
                                class="form-control"
                                id="age"
                                v-model="form.student.age"
                            />
                        </div>
                        <div class="form-group">
                            <label for="studentId">Student Id</label>
                            <input
                                type="text"
                                class="form-control"
                                id="studentId"
                                v-model="form.student.student_id"
                            />
                        </div>

                        <button type="submit" class="btn btn-primary">
                            Submit
                        </button>
                    </form>    
                </div>
                <div class="modal-footer">
                    <button
                        type="button"
                        class="btn btn-secondary"
                        v-on:click="closeModal"
                    >
                        Close
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from "axios";
export default {
    name: "student.create",

    //Components wich will be in this component
    components: {},

    //variables wich will be received
    props: {
        title: "",
    },

    //variables wich are use in this component
    data() {
        return {
            form: {
                student: {
                    firstname: "",
                    lastname: "",
                    email: "",
                    age: 0,
                    student_id: "",
                },
            },
            validationErrors: null,
        };
    },

    methods: {
        closeModal() {
            this.$emit("close-modal-create");
        },
        createStudent() {            
            axios
                .post("/students/create", this.form.student)
                .then((response) => {                    
                    this.$emit("close-modal-create");
                    this.$inertia.get(this.route("students.index"));
                })
                .catch((error) => {
                    if (error.response.status == 422) {
                        this.validationErrors = error.response.data.errors;
                    }
                });
        },
    },

    //variables that changed depending of other variables
    computed: {},

    //variables that changed depending of the change of a variable
    //also in watch we can to perform operations complex like calls http or asyn calls
    watch: {},
};
</script>

<style scoped></style>
