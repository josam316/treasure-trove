document.addEventListener('DOMContentLoaded', () => {
    const newTaskInput = document.getElementById('new-task');
    const addTaskButton = document.getElementById('add-task-button');
    const taskList = document.getElementById('task-list');

    addTaskButton.addEventListener('click', () => {
        const taskText = newTaskInput.value.trim();
        if (taskText) {
            addTask(taskText);
            newTaskInput.value = '';
        }
    });

    function addTask(taskText) {
        const taskItem = document.createElement('li');
        taskItem.className = 'task-item';
        taskItem.innerHTML = `
            <span>${taskText}</span>
            <div class="task-actions">
                <button class="complete">✔</button>
                <button class="edit">✎</button>
                <button class="delete">✖</button>
            </div>
        `;

        const completeButton = taskItem.querySelector('.complete');
        const editButton = taskItem.querySelector('.edit');
        const deleteButton = taskItem.querySelector('.delete');

        completeButton.addEventListener('click', () => {
            taskItem.classList.toggle('completed');
        });

        editButton.addEventListener('click', () => {
            const taskSpan = taskItem.querySelector('span');
            const newTaskText = prompt('Edit task:', taskSpan.textContent);
            if (newTaskText) {
                taskSpan.textContent = newTaskText;
            }
        });

        deleteButton.addEventListener('click', () => {
            taskList.removeChild(taskItem);
        });

        taskList.appendChild(taskItem);
    }
});
