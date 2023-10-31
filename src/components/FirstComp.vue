<template>
<nav class="navbar navbar-light bg-primary">
  <span class="navbar-brand mb-0 h1">To-Do's</span>
</nav>
<label for="todo">
  <h4>Enter To-do item:</h4>
</label>
<input type="text" name="todo" id="todo" v-model="item" />
<button v-on:click="add()">Add</button>

<h1><u>To-Do List</u></h1>

<table>
  <tr>
    <th>
      <h4>Description</h4>
    </th>
    <th>
      <h4>Action</h4>
    </th>
  </tr>
  <tr v-for="i in todo" :key="i">
    <td>{{ i.detail }} </td>
    <td><button class="two" v-on:click="deleteit(i.id)">
        <h6>Delete</h6>
      </button></td>
  </tr>
</table>
<button v-on:click="deleteall()" class="all">Delete all</button>
</template>

<script>
import axios from 'axios'
export default {
  name: 'FirstComp',
  data() {
    return {
      todo: [],
      item: '',

    }
  },
  async mounted() {
    const result = await axios.get("http://localhost:3000/todos");
    console.log(result)
    for (let i = 0; i < result.data.length; i++)
      this.todo.push(result.data[i])
  },
  methods: {
    async add() {
      // console.log(this.todo);
      const result = await axios.post("http://localhost:3000/todos", {
        detail: this.item
      })
      console.log(result)
    },
    async deleteall() {
      let id;
      const result = await axios.get("http://localhost:3000/todos");
      for (let i = 0; i < result.data.length; i++) {
        id = result.data[i].id;
        //  console.log(id)
        await axios.delete(`http://localhost:3000/todos/${id}`)
      }

    },
    async deleteit(id) {

      await axios.delete(`http://localhost:3000/todos/${id}`)
    }

  }

}
</script>

<style scoped>
h1 {
  margin-top: 50px;
  margin-left: 15px;
}

#todo {
  margin-top: 50px;
  margin-left: 10px;
}

button {
  margin-left: 10px;
  color: white;
  background-color: green;
  font-weight: bold;
  border-radius: 12px;
}

table,
tr,
th,
td {
  border: solid 2px black;
}

table {
  margin-left: 10px;

}

th {
  color: black;
  padding: 10px;
}

td {
  padding: 10px;
  color: rgb(70, 214, 86);
  font-weight: bold;
}

.two {
  color: white;
  background-color: blue;
  font-weight: bold;
  border-radius: 12px;
}

.all {
  color: white;
  background-color: red;
  font-weight: bold;
  border-radius: 12px;
  margin-top: 10px;
}
</style>
