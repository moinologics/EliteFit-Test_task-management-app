<template>
  <div class="max-w-6xl mx-auto p-6 bg-white shadow rounded">
    <div class="flex flex-col sm:flex-row gap-6">
      <!-- Left Column: Search, Filters, and Task Lists -->
      <div class="flex-1">
        <h1 class="text-2xl font-bold mb-4 text-center">Task Dashboard</h1>
        <!-- Search & Filters -->
        <div class="flex flex-col sm:flex-row gap-4 mb-6">
          <input
            type="text"
            v-model="searchTerm"
            placeholder="Search tasks..."
            class="border border-gray-300 rounded px-3 py-1 flex-1"
          />
          <select v-model="filterPriority" class="border border-gray-300 rounded px-3 py-1">
            <option>All</option>
            <option>High</option>
            <option>Medium</option>
            <option>Low</option>
          </select>
          <select v-model="filterStatus" class="border border-gray-300 rounded px-3 py-1">
            <option>All</option>
            <option>Completed</option>
            <option>Incomplete</option>
          </select>
        </div>
        <!-- Task Lists -->
        <div>
          <h2 class="text-xl font-semibold mt-6 mb-2">Upcoming Tasks</h2>
          <div v-if="upcomingTasks.length" class="space-y-4">
            <TaskItem 
              v-for="task in upcomingTasks" 
              :key="task.id" 
              :task="task" 
              @edit="editTask"
              @delete="deleteTask"
              @toggleComplete="toggleComplete"
            />
          </div>
          <p v-else class="text-gray-500">No upcoming tasks.</p>
        </div>

        <div>
          <h2 class="text-xl font-semibold mt-6 mb-2">Overdue Tasks</h2>
          <div v-if="overdueTasks.length" class="space-y-4">
            <TaskItem 
              v-for="task in overdueTasks" 
              :key="task.id" 
              :task="task" 
              @edit="editTask"
              @delete="deleteTask"
              @toggleComplete="toggleComplete"
            />
          </div>
          <p v-else class="text-gray-500">No overdue tasks.</p>
        </div>

        <div>
          <h2 class="text-xl font-semibold mt-6 mb-2">Completed Tasks</h2>
          <div v-if="completedTasks.length" class="space-y-4">
            <TaskItem 
              v-for="task in completedTasks" 
              :key="task.id" 
              :task="task" 
              @edit="editTask"
              @delete="deleteTask"
              @toggleComplete="toggleComplete"
            />
          </div>
          <p v-else class="text-gray-500">No completed tasks.</p>
        </div>
      </div>

      <!-- Right Column: Task Form -->
      <div class="w-full sm:w-1/3">
        <TaskForm :taskToEdit="taskToEdit" @saveTask="handleSaveTask" @cancelEdit="clearEdit" />
      </div>
    </div>
  </div>
</template>

<script>
import TaskForm from './TaskForm.vue'
import TaskItem from './TaskItem.vue'

export default {
  name: 'TaskDashboard',
  components: {
    TaskForm: TaskForm,
    TaskItem: TaskItem
  },
  data() {
    return {
      tasks: [],
      searchTerm: '',
      filterPriority: 'All',
      filterStatus: 'All',
      taskToEdit: null
    }
  },
  created() {
    this.loadTasks();
  },
  methods: {
    loadTasks() {
      const stored = localStorage.getItem('tasks');
      if (stored) {
        this.tasks = JSON.parse(stored);
      }
    },
    saveTasks() {
      localStorage.setItem('tasks', JSON.stringify(this.tasks));
    },
    addTask(task) {
      this.tasks.push(task);
      this.saveTasks();
    },
    updateTask(updatedTask) {
      const index = this.tasks.findIndex(
        (task) => task.id === updatedTask.id,
      );
      if (index !== -1) {
        this.tasks[index] = updatedTask;
        this.saveTasks();
      }
    },
    deleteTask(id) {
      this.tasks = this.tasks.filter((task) => task.id !== id);
      this.saveTasks();
    },
    toggleComplete(id) {
      const task = this.tasks.find((task) => task.id === id);
      if (task) {
        task.completed = !task.completed;
        this.saveTasks();
      }
    },
    editTask(task) {
      this.taskToEdit = task;
    },
    clearEdit() {
      this.taskToEdit = null;
    },
    handleSaveTask(task) {
      if (this.taskToEdit) {
        this.updateTask(task);
        this.clearEdit();
      } else {
        this.addTask(task);
      }
    },
    getToday() {
      return new Date().toISOString().split('T')[0];
    }
  },
  computed: {
    filteredTasks() {
      return this.tasks.filter((task) => {
        const matchesSearch =
          task.title.toLowerCase().indexOf(this.searchTerm.toLowerCase()) !== -1 ||
          task.description.toLowerCase().indexOf(this.searchTerm.toLowerCase()) !== -1;
        const matchesPriority =
          this.filterPriority === 'All' || task.priority === this.filterPriority;
        const matchesStatus =
          this.filterStatus === 'All' ||
          (this.filterStatus === 'Completed' ? task.completed : !task.completed);
        return matchesSearch && matchesPriority && matchesStatus;
      });
    },
    upcomingTasks() {
      return this.filteredTasks.filter(
        (task) => !task.completed && task.dueDate >= this.getToday(),
      );
    },
    overdueTasks() {
      return this.filteredTasks.filter(
        (task) => !task.completed && task.dueDate < this.getToday(),
      );
    },
    completedTasks() {
      return this.filteredTasks.filter((task) => task.completed);
    }
  }
}
</script>
