# Tasks Service

Source: https://developers.google.com/apps-script/advanced/tasks

## Overview

The Tasks service enables developers to integrate Google Tasks API functionality into Apps Script projects. According to the documentation, "The Tasks service lets you use the Google Tasks API in Google Apps Script. This API gives users the ability to manage their tasks in Gmail."

This is classified as an advanced service requiring explicit enablement before use.

## Key Features

- Manage task lists and individual tasks
- Read and write operations supported
- Full integration with Gmail task management
- Access to Tasks API v1 reference documentation

## Sample Operations

### List Task Lists
```javascript
function listTaskLists() {
  try {
    const taskLists = Tasks.Tasklists.list();
    if (!taskLists.items) {
      console.log("No task lists found.");
      return;
    }
    for (let i = 0; i < taskLists.items.length; i++) {
      const taskList = taskLists.items[i];
      console.log(
        'Task list with title "%s" and ID "%s" was found.',
        taskList.title,
        taskList.id,
      );
    }
  } catch (err) {
    console.log("Failed with an error %s ", err.message);
  }
}
```

### List Tasks
```javascript
function listTasks(taskListId) {
  try {
    const tasks = Tasks.Tasks.list(taskListId);
    if (!tasks.items) {
      console.log("No tasks found.");
      return;
    }
    for (let i = 0; i < tasks.items.length; i++) {
      const task = tasks.items[i];
      console.log(
        'Task with title "%s" and ID "%s" was found.',
        task.title,
        task.id,
      );
    }
  } catch (err) {
    console.log("Failed with an error %s", err.message);
  }
}
```

### Add Task
```javascript
function addTask(taskListId) {
  let task = {
    title: "Pick up dry cleaning",
    notes: "Remember to get this done!",
  };
  try {
    task = Tasks.Tasks.insert(task, taskListId);
    console.log('Task with ID "%s" was created.', task.id);
  } catch (err) {
    console.log("Failed with an error %s", err.message);
  }
}
```

## Resources

- **Sample Application**: Simple Tasks demo available on GitHub
- **API Reference**: [Tasks API v1 documentation](https://developers.google.com/tasks/v1/reference) (external — not scraped)
- **Support**: [Tasks support guide](https://developers.google.com/tasks/support) (external — not scraped)
</content>
