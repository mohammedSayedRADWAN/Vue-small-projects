<script setup>
import { ref } from 'vue';
const newTask = ref('');

const tasks=ref([])
// here push the data into the ref array

function addTask(){
  const text=newTask.value.trim();
  if(!text)return;
  tasks.value.push({
    id:Date.now(),
    text:text,
    completed:false,
    favorite:false,
    });
    newTask.value=''
  }

</script>
<template>
 <div id="wrapper">
  <h1>Todo App</h1>
  <div class="input-row">
    <!-- v- model it is way to binding data known as two binding way-->
    <input type="text" placeholder="add task here" v-model="newTask">
    <button>Add</button>
  </div>
 </div>
</template>

<style scoped>
.app{
  max-width: 500px;
  margin: 2rem auto;
  font-family: sans-serif;
  text-align: center;
}
.input-row{
  display: flex;
  gap:0.5rem;
  margin-bottom: 1rem;
}
input{
  flex-grow:1;
  padding:0.5rem;
  border-radius: 6px;
  border: 1px solid #ccc;

}
button{
  padding:0.5rem 1rem;
  border-radius: 6px;
  border: 1px solid #ccc;
  cursor: pointer;
}
</style>
