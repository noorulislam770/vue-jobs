<script>

export default { 
  data() {
    return {
      name : 'John Doe',
      status: 'active',
      tasks : ['task 1','task 2','task 3','task 4', 'task 5'],
      link : 'https://www.google.com',
    };
  },
  methods : {
    toggleStatus() {
      
      if (this.status == 'active') {
        this.status ='pending'
        
      }
      else if (this.status == 'pending'){
        this.status == 'inactive'
      }
      else {
        this.status = 'active'
      }
    },
  },
}

</script>


<template>
  <h1>Vue Jobs {{ name }}</h1>
  <!-- <p v-if="status === 'active'"> User is active</p>
  <p v-else-if="status === 'pending'"> User is pending </p>
  <p v-else="status"> user is inactive</p> -->
  <p>User is {{ this.status }}</p>
   
   <h3>Tasks</h3>
   <ul>
    <li v-for="task in tasks " :key="task">{{ task }}</li>
   </ul>

   <a :link="link">Click for google</a>
   <br>
   <button @click="toggleStatus">Change status</button>
</template>

<style>

</style>