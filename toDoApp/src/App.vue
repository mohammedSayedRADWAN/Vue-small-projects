<script setup>
import { ref , computed} from 'vue';
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
function removeTask(id){
  tasks.value=tasks.value.filter((t)=>t.id!=id)
}
const editingId=ref(null);
const buffering=ref('')
function editTask(task){
  editingId.value=task.id;
  buffering.value=task;
}
function canselEdit(){
  editingId.value=null;
  buffering.value=''
}
function finishEdit(task) {
  if (editingId.value!=task.id) {
    return;
  }
  const trimmed=buffering.value.text.trim();
  if (!trimmed) {
    removeTask(task.id);
  }else{
    task.text=trimmed;
  }
  canselEdit();
  
}
function favToggle(task) {
  task.favorite=!task.favorite;
  
}

//filters
const search=ref('')
const activeSearch=ref('All')
const filters=['All','Incompleted','Completed','Favorites']
const filterdTasks = computed(() => {
  return tasks.value.filter((t) => {
    const matchesSearch = t.text
      .toLowerCase()
      .includes(search.value.toLowerCase());

    if (activeSearch.value === 'Incompleted') {
      return matchesSearch && !t.completed;
    }

    if (activeSearch.value === 'Completed') {
      return matchesSearch && t.completed;
    }

    if (activeSearch.value === 'Favorites') {
      return matchesSearch && t.favorite;
    }

    return matchesSearch;
  });
});
</script>
<template>
 <div id="wrapper">
  <h1>Todo App</h1>
  <div class="input-row">
    <!-- v- model it is way to binding data known as two binding way-->
    <input type="text" placeholder="add task here" v-model="newTask">
    <button @click="addTask">Add</button>
  </div>
<!--search-->
<input type="text" placeholder="search here" v-model="search">
<div 
@click="activeSearch=f" 
class="filters" v-for="f in filters" 
:class="{activeSearch:activeSearch===f}"
:key="f">

{{ f }}
</div>

  <!--show tasks-->
  <ul class="task-list">
    <li v-for="task in filterdTasks" :key="task.id"  
    :class="{done:task.completed , editing:editingId==task.id}">

     <template v-if="editingId!=task.id">
      <button class="delete" @click="removeTask(task.id)">x</button>
      <button class="fav" @click="favToggle(task)">
        {{ task.favorite ? '⭐':'☆' }}
      </button>
      <input type="checkbox" v-model="task.completed">
      <span @click="editTask(task)">{{task.text}}</span>
     </template>

     <!--show editing parts if editingId==task.id-->
     <template v-else>
      <input type="checkbox" v-model="task.completed">
      <!--event directives and binding shourtcut ():)-->
      <input type="text" v-model="buffering.text" class="edit-inpu" 

      @keyup.enter="finishEdit(task)"  
      @keydown.esc="canselEdit"
      @blur="finishEdit(task)"
      :ref="(el)=>el&&el.focus()">
      <button class="save" @click="finishEdit(task)">save</button>
      <button class="cancel" @click="canselEdit()">cancel</button>
     </template>
      
    </li>
  </ul>
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
.filters {
  display: flex;
  gap: 0.5rem;
  margin: 1rem 0;
  flex-wrap: wrap;
}
.filters button.active {
  background: #333;
  color: #fff;
  border-color: #333;
}

.task-list {
  list-style: none;
  padding: 0;
}
.task-list li {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.5rem;
  border-bottom: 1px solid #eee;
}
.task-list li.done span {
  text-decoration: line-through;
  opacity: 0.6;
}

.fav {
  background: none;
  border: none;
  cursor: pointer;
}
.delete {
  background: #e53e3e;
  color: white;
  border: none;
  cursor: pointer;
}
.edit-input {
  flex-grow: 1;
}
</style>
