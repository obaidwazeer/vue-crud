<template>
    <div class="container mt-5">
        <div class="card">
            <div class="card-header">
                <h4>Edit Student</h4>
            </div>
            <div class="card-body">
                <div for="" class="mb-3">
                    <label>Name</label>
                    <input type="text" class="form-control" v-model="model.student.name" />
                </div>
                <div for="" class="mb-3">
                    <label>Email</label>
                    <input type="email" class="form-control" v-model="model.student.email" />
                </div>
                <div for="" class="mb-3">
                    <label>Course</label>
                    <input type="text" class="form-control" v-model="model.student.course" />
                </div>
                <div for="" class="mb-3">
                    <label>Phone</label>
                    <input type="text" class="form-control" v-model="model.student.phone" />
                </div>
                <div for="" class="mb-3">
                    <button type="button" class="btn btn-primary" @click="updateStudent">Update</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    name: 'editStudent',
    data() {
        return {
            student_id: '',
            model: {
                student: {
                    name: '',
                    email: '',
                    course: '',
                    phone: '',
                }
            }
        }
    },
    mounted(){
        this.student_id = this.$route.params.id;
        this.getSingleData(this.$route.params.id);
    },
    methods: {
        // mythis: this,
        getSingleData(student_id){
            axios.get(`http://127.0.0.1:8000/api/home/${student_id}/edit`).then(res => {
                console.log(res.data.student);
                this.model.student = res.data.student;
            });
        },
        updateStudent() {
            axios.put(`http://127.0.0.1:8000/api/home/${this.student_id}/edit` , this.model.student).then(res => {
                console.log(res.data.message);
            });
        }
    }
}
</script>
