# task_tracker
Task Tracker CLI Application

Developed a Command Line Interface (CLI) application using Python to efficiently manage tasks and to-do lists. The application enables users to add, view, and update tasks, providing a seamless way to keep track of their responsibilities. The project involved utilizing Python's file handling capabilities to ensure task data persistence. Users can assign priorities, due dates, and mark tasks as completed. The CLI application showcases my programming skills, user input processing, data storage management, and ability to create a user-friendly text-based interface. The codebase is available on GitHub as a testament to my practical coding proficiency.
import os
import json
from datetime import datetime

# File to store tasks
TASKS_FILE = "tasks.json"

# Load tasks from file
def load_tasks():
    if os.path.exists(TASKS_FILE):
        with open(TASKS_FILE, "r") as file:
            return json.load(file)
    return []

# Save tasks to file
def save_tasks(tasks):
    with open(TASKS_FILE, "w") as file:
        json.dump(tasks, file, indent=4)

# Add a new task
def add_task(tasks):
    task_name = input("Enter task name: ")
    priority = input("Enter task priority (low, medium, high): ").lower()
    due_date = input("Enter due date (YYYY-MM-DD): ")

    tasks.append({
        "name": task_name,
        "priority": priority,
        "due_date": due_date,
        "completed": False
    })

    save_tasks(tasks)
    print("Task added successfully!")

# List all tasks
def list_tasks(tasks):
    for index, task in enumerate(tasks, start=1):
        status = "Completed" if task["completed"] else "Pending"
        print(f"{index}. {task['name']} (Priority: {task['priority']}, Status: {status})")

# Mark a task as completed
def complete_task(tasks):
    list_tasks(tasks)
    task_index = int(input("Enter the index of the task to mark as completed: ")) - 1
    if 0 <= task_index < len(tasks):
        tasks[task_index]["completed"] = True
        save_tasks(tasks)
        print("Task marked as completed!")
    else:
        print("Invalid task index.")

# Main function
def main():
    tasks = load_tasks()

    while True:
        print("\nTask Tracker CLI Application")
        print("1. Add Task")
        print("2. List Tasks")
        print("3. Mark Task as Completed")
        print("4. Exit")
        choice = input("Enter your choice: ")

        if choice == "1":
            add_task(tasks)
        elif choice == "2":
            list_tasks(tasks)
        elif choice == "3":
            complete_task(tasks)
        elif choice == "4":
            print("Exiting the application.")
            break
        else:
            print("Invalid choice. Please select a valid option.")

if __name__ == "__main__":
    main()
