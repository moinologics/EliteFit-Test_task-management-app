<template>
  <div id="app" class="p-8 bg-gray-100 min-h-screen">
    <TaskDashboard />
  </div>
</template>

<script>
import TaskDashboard from './components/TaskDashboard.vue'

export default {
  name: 'App',
  components: {
    TaskDashboard
  }
}
</script>
