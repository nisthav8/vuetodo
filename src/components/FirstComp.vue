<template>
 <nav class="navbar navbar-light bg-primary">
    <span class="navbar-brand mb-0 h1">To-Do's</span>
  </nav>
<label for="todo"><h4>Enter To-do item:</h4></label>
  <input type="text" name="todo" id="todo" v-model="todo"/>
  <button v-on:click="add()" v>Add</button>

</template>

<script>


export default {
  name: 'FirstComp',
  data(){
return{
  todo:'',
}
  },
  methods:{
      add(){
        console.log(this.todo);
      }
  }

}
</script>

<style scoped>
#todo{
  margin-top:50px;
  margin-left:10px;
}
button{
  margin-left:10px;
  color:white;
  background-color: blue;
  font-weight: bold;
  border-radius: 12px;
}
</style>
