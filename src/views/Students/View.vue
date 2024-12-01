
<template>
    <div class="container">
        <div class="card">
            <div class="card-header">
                <h4>
                    Students
                    <RouterLink to="students/create" class="btn btn-primary float-end">Add Student</RouterLink>
                </h4>
            </div>
            <div class="card-body">
                <table class="table table-bordered">
                    <thead>
                        <tr>
                            <th>ID</th>
                            <th>Name</th>
                            <th>Email</th>
                            <th>Course</th>
                            <th>Created At</th>
                            <th>Action</th>
                        </tr>
                    </thead>
                    <tbody v-if="this.students.length > 0">
                        <tr v-for="(student, index) in this.students" :key="index">
                            <td>{{student.id}}</td>
                            <td>{{student.name}}</td>
                            <td>{{student.email}}</td>
                            <td>{{student.course}}</td>
                            <td>{{student.created_at}}</td>
                            <td>
                               <RouterLink :to="{ path:'students/' + student.id + '/edit' }" class="btn btn-success">Edit</RouterLink>
                                <button type="button" class="btn btn-danger" @click="deleteStudent(student.id)">Delete</button>
                            </td>

                        </tr>
                    </tbody>
                    <tbody v-else>
                        <tr>
                            <td class="colspan-7">Loading</td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>
</template>

<script>
    import axios from 'axios'

    export default{
        name: 'students',
        data(){
            return {
                students: []
            }
        },
        mounted(){
            // console.log('I am mounted');
            this.getStudents();
        },
        methods: {
            getStudents(){
                axios.get('http://127.0.0.1:8000/api/home').then(res => {
                    this.students = res.data.students;
                    console.log(this.students);
                });
            },
            deleteStudent(studentId){
                axios.delete(`http://127.0.0.1:8000/api/home/${studentId}/delete`).then(res => {
                    console.log(res);
                    this.getStudents();
                });
            }
        }
    }
</script>
  