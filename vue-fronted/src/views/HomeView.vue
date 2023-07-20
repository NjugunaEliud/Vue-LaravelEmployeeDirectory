<template>
  <div class="home">
 <h3>This website entails of employees signing in and out </h3>
  </div>
</template>

<script>


export default {
  components: {
    data(){
      return{
        results:{}
      }
    },
    created(){

    },
    methods:{
      saveEmployee(){
        const url=('http://127.0.0.1:8000/api/employees');
         axios.get(url)
         .then((data)=>{
          $this.results= data;
          console.log(data);
         })


      }

    }
    
  }
}
</script>
