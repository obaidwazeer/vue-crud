<template>
    <div class="container mt-5">
        <div class="card">
            <ul class="alert alert-warning" v-if="Object.keys(this.errorList).length > 0">
                <li class="mb-0 ms-3" v-for="(error, index) in this.errorList" :key="index">
                    {{ error[0]}}
                </li>
            </ul>
            <div class="card-header">
                <h4>Add Student</h4>
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
                    <button type="button" class="btn btn-primary" @click="saveStudent">Save</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    name: 'studentCreate',
    data() {
        
        return {
            errorList:'',
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
    methods: {
        // mythis: this,
        saveStudent() {
            var mythis = this;
            axios.post('http://127.0.0.1:8000/api/home', this.model.student).then(res => {
                console.log(res.data.message);
                this.model.student = {
                    name: '',
                    email: '',
                    course: '',
                    phone: '',
                }
            });
            // .catch(function (error) {
            //     if (error.response) {
            //         if(error.response.status == 422){
            //             mythis.errorList = error.response.data.message;
            //         }
            //     }
            // });
        }
    }
}
</script>
