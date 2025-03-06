<template>
  <div class="bg-white p-4 shadow rounded flex flex-col sm:flex-row justify-between items-start sm:items-center mb-4">
    <div class="flex-1">
      <h3 :class="['text-lg font-semibold', task.completed ? 'line-through text-gray-500' : '']">
        {{ task.title }}
      </h3>
      <p class="text-gray-700">{{ task.description }}</p>
      <p class="text-sm text-gray-600">Due: {{ task.dueDate }}</p>
      <p class="text-sm text-gray-600">Priority: {{ task.priority }}</p>
      <p class="text-sm text-gray-600">
        Status: {{ task.completed ? 'Completed' : 'Incomplete' }}
      </p>
    </div>
    <div class="mt-3 sm:mt-0 flex gap-2">
      <button
        @click="$emit('toggleComplete', task.id)"
        class="bg-green-500 hover:bg-green-600 text-white px-3 py-1 rounded text-sm"
      >
        {{ task.completed ? 'Mark Incomplete' : 'Mark Complete' }}
      </button>
      <button
        @click="$emit('edit', task)"
        class="bg-blue-500 hover:bg-blue-600 text-white px-3 py-1 rounded text-sm"
      >
        Edit
      </button>
      <button
        @click="$emit('delete', task.id)"
        class="bg-red-500 hover:bg-red-600 text-white px-3 py-1 rounded text-sm"
      >
        Delete
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TaskItem',
  props: {
    task: {
      type: Object,
      required: true
    }
  }
}
</script>
