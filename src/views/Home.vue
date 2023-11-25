<!-- döngülerde bizden key istenir -->
<template>
  <div class="Home">
   <h1>Home</h1> 
   <div v-if="users.length">
    <div v-for="user in users" :key="user.id">
      <SingleProject :user="user" @delete="handleDelete" @complete="handleComplete"></SingleProject>
    </div> 
   </div>
  </div>
</template>

<script> 
import SingleProject from '../components/SingleProject.vue'
  
export default {
  name: 'Home',
  components: {SingleProject},
  data(){
    return{
      users:[]
    }
  },
  mounted(){
    //jsonu okudum
   fetch('http://localhost:3000/users')
   .then(res=>res.json())
   .then(data=>this.users=data)
   .catch((err)=> console.log(err.message))
  },
  methods:{
handleDelete(id){
  this.users=this.users.filter((user)=>user.id!== id)
},
handleComplete(id)  {
let p=this.users.find((user)=>user.id===id)
p.complete=!p.complete;
}
  }
}
</script>
