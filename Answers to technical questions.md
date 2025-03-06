## How long did you spend on the coding test? 
4-5 hours

## What was the most useful feature that was added to the latest version of your chosen language? Please include a snippet of code that shows how you've used it.
I'd say one of the most useful additions is the **Teleport** feature. It’s a real game-changer for handling UI elements like modals, tooltips, or notifications that need to be rendered outside their usual parent hierarchy. It makes managing z-index and layout much simpler, allowing these elements to be placed at a more convenient spot in the DOM (for example, right under the `<body>` tag).

Here’s a snippet of how I’ve used Teleport in a project:

```vue
<template>
  <div>
    <button @click="showModal = true" class="bg-blue-500 text-white px-4 py-2 rounded">
      Open Modal
    </button>
    <teleport to="body">
      <div v-if="showModal" class="fixed inset-0 flex items-center justify-center bg-black bg-opacity-50">
        <div class="bg-white p-6 rounded shadow-lg">
          <p>This is a modal rendered with Teleport!</p>
          <button @click="showModal = false" class="mt-4 bg-red-500 text-white px-4 py-2 rounded">
            Close
          </button>
        </div>
      </div>
    </teleport>
  </div>
</template>

<script>
export default {
  name: 'TeleportExample',
  data: function () {
    return {
      showModal: false
    }
  }
}
</script>
```

In this example, the modal content is defined within the component but rendered directly into the `<body>`, which simplifies styling and avoids potential overflow or stacking context issues. This flexibility has made UI development much smoother in our projects.


## How would you track down a performance issue in production? Have you ever had to do this?
Here's how I'd approach tracking down a performance issue in production

1. **Monitoring and Data Collection:**  
  First, I’d start by gathering as much information as possible. I’d check the monitoring dashboards to see if there are any unexpected spikes in CPU usage, memory, or network traffic. I usually take a good look at the logs as well—sometimes a few error messages or warnings can provide early hints of what’s going wrong. I also value user feedback; if several people mention that a particular page or feature is lagging, that’s a strong clue to where I should dig in.

2. **Instrumentation and Tracing:**  
  Next, I’d move on to tracing the flow of requests through the system. Using Application Performance Monitoring tools, I can see how a request moves from one part of the system to another. This helps me pinpoint any slow spots—whether it’s a lag in the backend code, a sluggish database query, or even delays when calling an external API. In more complex, microservices-based environments, I’d use distributed tracing to follow the journey of a request across multiple services, which really helps in identifying exactly where the bottleneck is.

3. **Identifying and Isolating the Problem:**  
  Once I have all this data, the next step is to isolate the issue. I typically run a performance profiler to see which functions or operations are taking too long. Sometimes comparing these findings with data from a staging or development environment helps me understand whether the problem is specific to production. This phase is all about narrowing down the exact part of the system that’s causing the slowdown, so I can then focus on optimizing that part.

This hands-on, step-by-step approach helps me get to the root of the issue efficiently while ensuring I have all the context I need from real-world usage.

### My experience

I have encountered a similar situation in production. We had some APIs that were really sluggish, and after digging into the query logs and performance metrics on MongoDB Atlas, I discovered that a few long-running aggregation queries were the main culprits. Once I identified these, we restructured our approach by splitting the heavy aggregation into multiple smaller queries. This change significantly improved the API response times and underscored the importance of detailed performance monitoring and iterative query optimization.


## If you had more time, what additional features or improvements would you consider adding to the task management application?
 - Recurring Tasks: Add the ability to create recurring tasks, such as weekly or monthly reminders.
 - Notifications and Reminders: Integrate local notifications to alert users when deadlines are approaching or tasks are overdue.
 - Task Categorization and Tagging: Allow users to group tasks by category or tag, making it easier to sort and filter tasks beyond just priority and status.