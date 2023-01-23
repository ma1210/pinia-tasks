<template>
  <main>

    <!-- heading -->
    <header>
      <img src="https://pinia.vuejs.org/logo.svg" alt="pinia logo">
      <h1>Pinia Tasks</h1>
    </header>

    <!-- Task Form -->
    <div class="new-task-form">
      <TaskForm/>
    </div>

    <!-- filter -->
    <nav class="filter">
      <button @click="filter = 'all'">All tasks</button>
      <button @click="filter = 'favs'">Fav tasks</button>
    </nav>

    <!-- Loading -->
    <div class="loading" v-if="loading">Loading tasks...</div>

    <!-- task list -->
    <div class="task-list" v-if="filter === 'all'">
      <p>You have {{ totalCount }} tasks left to do</p>
      <div v-for="task in tasks">
        <TaskDetails :task="task"/>
      </div>
    </div>

    <div class="task-list" v-if="filter === 'favs'">
      <p>You have {{ favCount }} favs tasks left to do</p>
      <div v-for="task in favs">
        <TaskDetails :task="task"/>
      </div>
    </div>

    <button @click="taskStore.$reset">reset state</button>

  </main>
</template>

<script>
  import TaskDetails from './components/TaskDetails.vue'
  import { useTaskStore } from './stores/TaskStore';
  import { ref } from 'vue';
  import TaskForm from './components/TaskForm.vue';
import { storeToRefs } from 'pinia';

  export default {
    components:{ TaskDetails, TaskForm }, 
    setup() {
      const taskStore = useTaskStore()

      const { tasks, loading, favs, totalCount, favCount } = storeToRefs(taskStore)

      taskStore.getTasks()

      const filter = ref('all')

      return { taskStore, filter, tasks, loading, favs, totalCount, favCount }
    }
  }
</script>