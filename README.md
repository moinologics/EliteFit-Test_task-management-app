# Task Management Application (EliteFit Test)

A simple task management application built with Vue.js and Tailwind CSS. This app allows users to manage tasks by adding, editing, deleting, and filtering them. Tasks are organized into sections: Upcoming, Overdue, and Completed. The application uses the browser's localStorage for data persistence.

## Overview

This project was developed as a coding test to create a straightforward and user-friendly task management tool. The application provides:

- **Task Management:** Create, update, and delete tasks.
- **Categorized Lists:** Tasks are automatically sorted into Upcoming, Overdue, and Completed sections.
- **Search & Filter:** Easily search for tasks and filter by priority (High, Medium, Low) and completion status.
- **Responsive Design:** Clean and responsive interface built with Tailwind CSS.
- **Local Storage:** Data is stored locally on the user's browser, eliminating the need for a backend.

## Features

- **Task Dashboard:** Displays lists for upcoming, overdue, and completed tasks.
- **Task Form:** A form for adding and editing tasks.
- **Task Item:** Individual task component with options to mark as complete/incomplete, edit, or delete.
- **Search & Filters:** Quickly find tasks by title or description and filter by priority and status.

## Setup Instructions

### Prerequisites

- Node.js (version 20 or higher)
- npm

### Installation

1. **Clone the Repository:**

    ```bash
    git clone https://github.com/moinologics/EliteFit-Test_task-management-app.git
    cd EliteFit-Test_task-management-app
    ```

2. **Install Dependencies:**

    ```bash
    npm install
    ```

3. **Run the Development Server:**

    ```bash
    npm run dev
    ```

4. **View the Application:**

   Open your browser and navigate to `http://localhost:5173` (or the port indicated in your terminal) to see the application in action.

## Project Structure

- `src/App.vue` - Main application component.
- `src/components/TaskDashboard.vue` - Dashboard containing search, filters, and task lists.
- `src/components/TaskForm.vue` - Form component for adding and editing tasks.
- `src/components/TaskItem.vue` - Component for rendering individual tasks.
- `README.md` - Project overview and setup instructions.

## Assumptions Made

- **Data Storage:** The app uses browser localStorage for simplicity, assuming that client-side persistence meets the project requirements.
- **UI Complexity:** The design is focused on core functionality with a minimalistic UI. Advanced features like drag-and-drop or external APIs are outside the current scope.
- **Task Attributes:** Each task includes a title, description, due date, priority, and completion status, which are deemed sufficient for this application.
- **Browser Support:** The app is targeted at modern browsers that support ES6 and current web standards.
- **Error Handling:** Basic form validations and error alerts are implemented, while comprehensive error handling is not in scope.

## Additional Information

- This project was built to showcase proficiency in Vue.js, Tailwind CSS, and client-side development.
- Feel free to extend the functionality by integrating backend services, adding user authentication, or implementing advanced features.
