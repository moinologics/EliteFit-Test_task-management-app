<template>
  <div class="bg-white shadow rounded p-6 mb-6">
    <h2 class="text-lg font-bold mb-4">
      {{ taskToEdit ? 'Edit Task' : 'Add New Task' }}
    </h2>
    <form @submit.prevent="onSubmit" class="space-y-4">
      <div>
        <label for="title" class="block font-medium mb-1">Title:</label>
        <input
          type="text"
          id="title"
          v-model="task.title"
          required
          class="w-full border border-gray-300 rounded px-3 py-2 focus:outline-none focus:ring focus:border-blue-300"
        />
      </div>
      <div>
        <label for="description" class="block font-medium mb-1">Description:</label>
        <textarea
          id="description"
          v-model="task.description"
          class="w-full border border-gray-300 rounded px-3 py-2 focus:outline-none focus:ring focus:border-blue-300"
        ></textarea>
      </div>
      <div>
        <label for="dueDate" class="block font-medium mb-1">Due Date:</label>
        <input
          type="date"
          id="dueDate"
          v-model="task.dueDate"
          required
          class="w-full border border-gray-300 rounded px-3 py-2 focus:outline-none focus:ring focus:border-blue-300"
        />
      </div>
      <div>
        <label for="priority" class="block font-medium mb-1">Priority:</label>
        <select
          id="priority"
          v-model="task.priority"
          required
          class="w-full border border-gray-300 rounded px-3 py-2 focus:outline-none focus:ring focus:border-blue-300"
        >
          <option value="High">High</option>
          <option value="Medium">Medium</option>
          <option value="Low">Low</option>
        </select>
      </div>
      <div class="flex gap-4">
        <button
          type="submit"
          class="bg-blue-500 hover:bg-blue-600 text-white px-4 py-2 rounded"
        >
          {{ taskToEdit ? 'Update Task' : 'Add Task' }}
        </button>
        <button
          v-if="taskToEdit"
          type="button"
          @click="onCancel"
          class="bg-gray-500 hover:bg-gray-600 text-white px-4 py-2 rounded"
        >
          Cancel
        </button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: 'TaskForm',
  props: {
    taskToEdit: {
      type: Object,
      default: null
    }
  },
  data() {
    return {
      defaultTask: {
        id: null,
        title: '',
        description: '',
        dueDate: '',
        priority: 'Medium',
        completed: false,
      },
      task: {
        id: null,
        title: '',
        description: '',
        dueDate: '',
        priority: 'Medium',
        completed: false,
      }
    }
  },
  watch: {
    taskToEdit: {
      handler(newVal) {
        if (newVal) {
          this.task = Object.assign({}, newVal);
        } else {
          this.task = Object.assign({}, this.defaultTask);
        }
      },
      immediate: true
    }
  },
  methods: {
    onSubmit() {
      if (!this.task.title || !this.task.dueDate || !this.task.priority) {
        alert('Please fill in required fields.');
        return;
      }
      if (!this.task.id) {
        this.task.id = Date.now();
      }
      this.$emit('saveTask', Object.assign({}, this.task));
      if (!this.taskToEdit) {
        this.task = Object.assign({}, this.defaultTask);
      }
    },
    onCancel() {
      this.$emit('cancelEdit');
      this.task = Object.assign({}, this.defaultTask);
    }
  }
}
</script>
