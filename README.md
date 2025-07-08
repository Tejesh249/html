<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>To-Do List App</title>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/css/bootstrap.min.css">
    <style>
        body {
            background-color: #f0f0f0;
        }
    </style>
</head>
<body>
    <div class="container mt-5">
        <h1 class="text-center mb-4">To-Do List App</h1>
        <div class="row justify-content-center">
            <div class="col-md-8">
                <div class="card">
                    <div class="card-body">
                        <input type="text" id="task-input" class="form-control mb-3" placeholder="Add new task">
                        <button id="add-task-btn" class="btn btn-primary mb-3">Add Task</button>
                        <ul id="task-list" class="list-group">
                        </ul>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/js/bootstrap.bundle.min.js"></script>
    <script>
        let tasks = [];
        const taskList = document.getElementById('task-list');
        const taskInput = document.getElementById('task-input');
        const addTaskBtn = document.getElementById('add-task-btn');

        addTaskBtn.addEventListener('click', addTask);

        function addTask() {
            const task = taskInput.value.trim();
            if (task) {
                tasks.push({ text: task, id: Date.now() });
                taskInput.value = '';
                renderTaskList();
            }
        }

        function renderTaskList() {
            taskList.innerHTML = '';
            tasks.forEach(task => {
                const taskItem = document.createElement('li');
                taskItem.classList.add('list-group-item');
                taskItem.innerHTML = `
                    <span>${task.text}</span>
                    <div class="float-end">
                        <button class="btn btn-sm btn-primary" onclick="editTask(${task.id})">Edit</button>
                        <button class="btn btn-sm btn-danger" onclick="deleteTask(${task.id})">Delete</button>
                    </div>
                `;
                taskList.appendChild(taskItem);
            });
        }

        function editTask(id) {
            const taskIndex = tasks.findIndex(task => task.id === id);
            if (taskIndex !== -1) {
                const newTask = prompt('Enter new task text');
                if (newTask) {
                    tasks[taskIndex].text = newTask;
                    renderTaskList();
                }
            }
        }

        function deleteTask(id) {
            const taskIndex = tasks.findIndex(task => task.id === id);
            if (taskIndex !== -1) {
                tasks.splice(taskIndex, 1);
                renderTaskList();
            }
        }
    </script>
</body>
</html>
