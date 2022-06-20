<template>
 <div class="container p-4 text-center">
   <form class="w-75" @submit.prevent="createTodo()">
     <div class="form-group">
       <label for="">Todo</label>
       <input 
       v-model="todo.title"
       type="text"  class="form-control" placeholder="" aria-describedby="helpId">
       <small id="helpId" class="text-muted">Create You New Todo</small>
     </div>
     <div class="form-group">
       <label for="">Description</label>
       <textarea 
       v-model="todo.des"
       class="form-control" rows="3"></textarea>
     </div>
     <br>
     <div class="form-group">
       <button class="btn btn-primary" type="submit"> Add Todo </button>
     </div>
   </form>
   <section class="mt-3 border-primary">
     <ul class="list-group">
     <li v-for='(todo,i) in allTodo'
       class="list-group-item position-relative">
     
     <div class="d-flex justify-content-around w-100">
     <button @click="xyz(todo)"
     v-if="!todo.done"
     class="btn btn-danger" 
     type="button">DONE</button>
     <button class="badge bg-info" type="button"
      @click="xxc(i)"
      >Delete</button>
     <span
     :class="{isdone:todo.done}"
     >{{todo.title}}</span>
     </div>
     </li>
     </ul>
   </section>
 </div>
</template>
<script>

export default {
  
   data :()=>({
    todo :{
       title:'',
       des:'',
       done:false,
    },
    allTodo:[]
   })
   ,
   watch:{
     allTodo:
       {
         handler(){
          //  this.allTodo.map((todo)=>{
          //    localStorage.todo=JSON.stringify(todo)
          //  })
           localStorage.todo=JSON.stringify(this.allTodo)
         },
         deep:true
       }
     
   },mounted(){
     if(localStorage.todo){
       this.allTodo=JSON.parse(localStorage.todo)
     }
   }
    ,
   methods:{
     createTodo(){
        const {title,des}=this.todo
         this.allTodo.push({title,des})
        this.todo.title=''
        this.todo={} 
     },
     xyz(todo){
       todo.done=true
     },
     xxc(i){
       this.allTodo.splice(i,1)
       console.log(this.allTodo);
     }
   }
    
  }
</script>
<style>
.isdone {
  text-decoration: line-through;
}
</style>