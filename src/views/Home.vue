<template>
    <div v-show="showAddTask">
        <AddTask @add-task="addTask" />
    </div>
    <Tasks :tasks="tasks" @delete-task="deleteTask" @toggle-reminder="toggleReminder" />
</template>

<script>
    import Tasks from '../components/Tasks';
    import AddTask from '../components/AddTask';

    export default {
        name: 'Home',
        props: {
            showAddTask: Boolean,
        },
        components: {
            Tasks,
            AddTask,
        },
        data() {
            return {
                tasks: [],
            };
        },
        methods: {
            async addTask(newTask) {
                const res = await fetch('http://localhost:5000/tasks', {
                    method: 'POST',
                    headers: {
                        'Content-type': 'application/json',
                    },
                    body: JSON.stringify(newTask),
                });

                const data = await res.json();
                this.tasks = [...this.tasks, data];
            },
            async deleteTask(taskId) {
                const res = await fetch(`http://localhost:5000/tasks/${taskId}`, {
                    method: 'DELETE',
                });

                if (res.status === 200) {
                    this.tasks = this.tasks.filter((task) => {
                        return task.id !== taskId;
                    });
                } else {
                    alert('Ooops! Task was not deleted');
                }
            },
            async toggleReminder(taskId) {
                const taskToToggle = await this.getTask(taskId);
                const updatedTask = { ...taskToToggle, reminder: !taskToToggle.reminder };
                const res = await fetch(`http://localhost:5000/tasks/${taskId}`, {
                    method: 'PUT',
                    headers: {
                        'Content-type': 'application/json',
                    },
                    body: JSON.stringify(updatedTask),
                });
                const data = await res.json();
                this.tasks = this.tasks.map((task) => {
                    return task.id == taskId ? { ...task, reminder: data.reminder } : task;
                });
            },
            async getAllTasks() {
                const res = await fetch('http://localhost:5000/tasks');
                const data = await res.json();
                return data;
            },
            async getTask(taskId) {
                const res = await fetch(`http://localhost:5000/tasks/${taskId}`);
                const data = await res.json();
                return data;
            },
        },
        async created() {
            this.tasks = await this.getAllTasks();
        },
    };
</script>
