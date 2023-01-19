<template>
  <main>

    <!-- heading -->
    <header>
      <img src="https://pinia.vuejs.org/logo.svg" alt="pinia logo">
      <h1>Pinia Tasks</h1>
    </header>

    <button @click="filter = 'all'">
      Display All
    </button>
    <button @click="filter = 'favs'">
      Display Favs
    </button>

    <!-- task list -->
    <div class="task-list" v-if="filter === 'all'">
      <p>All tasks</p>
      <div v-for="task in taskStore.tasks">
        <TaskDetails :task="task"/>
      </div>
    </div>

    <div class="task-list" v-if="filter === 'favs'">
      <p>Favourite Tasks</p>
      <div v-for="task in taskStore.favs">
        <TaskDetails :task="task"/>
      </div>
    </div>

  </main>
</template>

<script>
  import TaskDetails from './components/TaskDetails.vue'
  import { useTaskStore } from './stores/TaskStore';
  import { ref } from 'vue';

  export default {
    components:{ TaskDetails }, 
    setup() {
      const taskStore = useTaskStore()

      const filter = ref('all')

      return { taskStore, filter }
    }
  }
</script>