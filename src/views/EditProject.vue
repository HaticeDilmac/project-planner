<template>
    <form @submit.prevent="handleSubmit">
      <label>Title:</label>
      <input type="text" v-model="title" required>
      <label>Details:</label>
      <textarea v-model="details" required></textarea>
      <button>Update Project</button>
    </form>
  </template>
  
  <script>
  export default {
    props: ["id"],
    data() {
      return {
        title: "",
        details: "",
      };
    },
    computed: {
      uri() {
        return "http://localhost:3000/users/" + this.id;
      },
    },
    mounted() {
    //burada title ve details alanlarını datadan gelnlerle doldur
      fetch(this.uri)
        .then((res) => res.json())
        .then((data) => {
          this.title = data.title;
          this.details = data.details;
        });
    },
    methods:{
    handleSubmit(){
        let user={
               title: this.title,
               details:this.details,
               complete: false
            } 
            fetch(this.uri,{
                method:"PATCH",
                headers:{"Content-Type":"application/json"},
                body:JSON.stringify(user),
            })
            .then(()=>this.$router.push("/"))
            .catch((err)=>console.log)  
    }
    }
  };
  </script>
  
  <style>
  </style>
  