<template>
    <div
        class="modal fade show"
        id="modalUpdate"
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
                        Update student
                    </h5>
                </div>
                <div class="modal-body">
                    <form @submit.prevent="updateStudent">
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
                            Update
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
export default {
    name: "student.create",

    //Components wich will be in this component
    components: {},

    //variables wich will be received
    props: {
        studentValues: Object,
    },

    //variables wich are use in this component
    data() {
        return {
            form: {
                student: {
                    firstname: this.studentValues.firstname,
                    lastname: this.studentValues.lastname,
                    email: this.studentValues.email,
                    age: this.studentValues.age,
                    student_id: this.studentValues.student_id,
                },
            },
        };
    },

    methods: {
        closeModal() {
            this.$emit("close-modal-update");
        },
        updateStudent() {
            this.$inertia.put(
                this.route("students.update", this.studentValues),
                this.form.student
            );
            this.$emit("close-modal-update");
        },
    },

    //variables that changed depending of other variables
    computed: {},

    //variables that changed depending of the change of a variable
    //also in watch we can to perform operations complex like calls http or asyn calls
    watch: {},
};
</script>

<style scoped>
</style>
