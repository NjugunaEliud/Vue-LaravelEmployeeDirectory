<template>
  
  <div class="employee">
 <h3>Registered Employees</h3>
 <table class="table table-striped" >
  <thead>
    <tr>
      <th scope="col">ID</th>
      <th scope="col">Name</th>
      <th scope="col">Address</th>
      <th scope="col">Contact</th>

    </tr>
  </thead>
  <tbody>
    <tr v-for="employee in results" :key="employee.id">
      <td>{{employee.id}}</td>
      <td>{{employee.name}}</td>
      <td>{{employee.address}}</td>
      <td>{{employee.mobile}}</td>
     
    </tr>
  </tbody>
</table>
<router-link :to="{name:'register'}"><button class="btn btn-outline-warning">Register</button></router-link>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      results: {}
    };
  },
  created() {
    this.saveEmployee();
  },
  methods: {
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
      const upd="http://127.0.0.1:8000/api/update/" + this.employee.id;
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
    }
  }
};

</script>

<style>

</style>