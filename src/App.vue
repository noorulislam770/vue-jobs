
<script setup>
    import { ref, onMounted } from 'vue'


    const name = ref( 'John Doe');
    const status = ref('active');
    const tasks = ref(['task 1','task 2','task 3','task 4', 'task 5']);
    const link = ref('https://www.google.com');
    const newTask = ref('');







    const toggleStatus = () => {

        if (status.value == 'active') {
            status.value ='pending'    
        }
        else if (status.value == 'pending'){
            status.value = 'inactive'
        }
        else {
            status.value = 'active'
        }
    };

    const addTask = () => {
        if (newTask.value.trim() !== '') {
            tasks.value.push(newTask.value)
            newTask.value = '';
        }
    }
        
    const deleteTask = (index) => {
        tasks.value.splice(index,1);
    }

    onMounted( async () => {
        try {
            const response = await fetch('https://jsonplaceholder.typicode.com/todos');
            const data = await response.json();
            tasks.value = data.map((task) => task.title)
        }
        catch (error) {
            console.log('error fetching data');
        }
    }) 
</script>
 

<template>
  <h1>Vue Jobs {{ name }}</h1>
  <!-- <p v-if="status === 'active'"> User is active</p>
  <p v-else-if="status === 'pending'"> User is pending </p>
  <p v-else="status"> user is inactive</p> -->
  <p>User is {{ status }}</p>
    <form @submit.prevent="addTask">
        <label for="newTask">Add a new task: </label>
        <input type="text" id="newTask" name="newTask" v-model="newTask">
        <button type="submit">Submit</button>
    </form>
   <h3>Tasks</h3>
   <ul>
    <li v-for="(task, index) in tasks " :key="task">
        <span>
            {{ task }}
        </span>
        <button @click="deleteTask(index)">x</button>
    </li>
    </ul>

   <a :link="link">Click for google</a>
   <br>
   <button @click="toggleStatus">Change status</button>
</template>

<style>

</style>  