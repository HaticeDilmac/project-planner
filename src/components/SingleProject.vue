
<template>
  <div class="user" :class="{complete:user.complete}">
    <div class="actions">
      <h3>{{ user.id }}</h3>
      <h1 @click="showDetails=!showDetails">{{ user.title }}</h1>
        <div class="icons">
       <router-link :to="{name:'EditProject',params:{ id: user.id }}">
       <span class="material-icons">edit</span>
      </router-link>
          <span @click="deleteProject" class="material-icons">delete</span>
          <span @click="toggleComplete" class="material-icons">done</span>
       </div>
   </div> 
   <div v-if="showDetails" class="details">
    <!-- <h3>{{ user.details }}</h3> -->
    <p>{{ user.details }}</p>
   </div>  
  </div>
</template>

<script> 

 

export default {
props:["user"],
data(){
return{
  showDetails:false, 
  uri:'http://localhost:3000/'+this.user
}},
methods:{
 deleteProject(){
  fetch(this.uri,{method:"DELETE"})
  .then(()=>this.$emit("delete",this.user.id))
  .catch((err)=>console.log(err))
 },

 toggleComplete(){
  fetch(this.uri,{
    method:"PATCH",
    headers:{'Content-Type':'application/json'}, 
    body:JSON.stringify({complete:!this.user.complete})
  })
  .then(()=> this.$emit("complete",this.user.id))
  .catch((err)=>console.log(err))
 }
 }
}
</script>

<style>
.user{
  margin: 20px;
  background: #fff;
  padding: 20px;
  border-radius: 5px;
  box-shadow: 1px 2px 3px rgba(81, 81, 81, 0.05);
  border-left: 4px solid #e90074;
}
.actions{
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.material-icons{
  font-size: 20px;
  margin-left:  10px;
  color: #6e6b6b;
  cursor: pointer;
}
.material-icons:hover{
color: #e90074;
}
.user.complete{
  border-left: 4px solid rgb(12, 233, 0);
}
/* justify-content=mainAxisAlignment */
</style>