<template>
<div class="row">
<div class="col-6 col-md-4">
<h3>Register here</h3>
 <form class="m-4 me-4" @submit.prevent="saveData">
  <div class="form-group">
    <label for="exampleInputEmail1">Name :</label>
    <input type="text"  v-model="employee.name" class="form-control"  placeholder="Enter your name">
  </div>
  <div class="form-group">
    <label for="exampleInputEmail1">Address:</label>
    <input type="text" v-model="employee.address"  class="form-control"  placeholder="Enter Address">
  </div>
  <div class="form-group">
    <label for="exampleInputEmail1">Contact</label>
    <input type="text" class="form-control"  v-model="employee.mobile"  placeholder="Enter your Contact">
  </div>
  <button type="submit" class="btn btn-outline-success mt-2">Submit</button>
</form>
</div>
  <div class="col-12 col-md-8">
    <h3>Employees</h3>
 <table class="table table-striped" >
  <thead>
    <tr>
      <th scope="col">ID</th>
      <th scope="col">Name</th>
      <th scope="col">Address</th>
      <th scope="col">Contact</th>
      <th>Option</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="employee in results" :key="employee.id">
      <td>{{employee.id}}</td>
      <td>{{employee.name}}</td>
      <td>{{employee.address}}</td>
      <td>{{employee.mobile}}</td>
  
      <td>
        <router-link :to="{name:'register', params:{id:employee.id}}"><button class="btn btn-outline-warning"  @click="edit(employee)">Edit</button></router-link>
        <button class="btn btn-outline-danger ms-2"  @click="deletee(employee)" >Delete</button>
      </td>
    </tr>
  </tbody>
 </table>
  </div>
  
</div>
  
 
</template>

<script>
import axios from 'axios';

export default {
    data(){
        return{
            filters: {
            formatDate(timestamp) {
                const date = new Date(timestamp);
                return date.toLocaleString();
            }
            },

            results:{},
            employee:{
                id:'',
                name:'',
                address:'',
                mobile:''
            }
        }
    },
     created() {
    this.saveEmployee();
  },
    methods:{
        saveData(){
            this.save();
        },
        save(){
            const url= "http://127.0.0.1:8000/api/save"
            axios.post(url,this.employee)
            .then(({data})=>{
                alert('Data Saved Successfully');
                this.saveEmployee()

            })

        },
        saveEmployee() {
      const url = 'http://127.0.0.1:8000/api/employees';
      axios.get(url)
        .then(({ data }) => {
          this.results = data;
          console.log(data);
        })
        .catch(error => {
          console.log(error);
        });
    },
    edit(employee){
      this.employee=employee;
    },
    update(){
      const upd="http://127.0.0.1:8000/api/update/" + employee.id;
      axios.put(upd , this.employee)
      .then(
        ({data})=>{
          this.employee.name="";
          this.employee.address="";
          this.employee.mobile="";
          alert("Details updated")
          this.saveEmployee();

        }
      )
    },
   
   deletee(employee) {
  const upd = "http://127.0.0.1:8000/api/delete/" + employee.id;
  axios
    .delete(upd)
    .then(response => {
      alert('Employee Deleted');
      this.saveEmployee();
    })
    .catch(error => {
      console.error('Error deleting employee:', error);
      alert('Failed to delete employee. Please try again later.');
    });
}

  }
    }

</script>

<style>

</style>