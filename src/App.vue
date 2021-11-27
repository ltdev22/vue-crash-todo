<template>
    <div class="container">
        <Header
            @toggle-add-task="toggleAddTask"
            appTitle="Task Tracker"
            :showAddTask="showAddTask"
        />
        <div v-show="showAddTask">
            <AddTask @add-task="addTask" />
        </div>
        <Tasks :tasks="tasks" @delete-task="deleteTask" @toggle-reminder="toggleReminder" />
        <router-view></router-view>
        <Footer />
    </div>
</template>

<script>
    import Header from './components/Header';
    import Footer from './components/Footer';
    import Tasks from './components/Tasks';
    import AddTask from './components/AddTask';

    export default {
        name: 'App',
        components: {
            Header,
            Footer,
            Tasks,
            AddTask,
        },
        data() {
            return {
                tasks: [],
                showAddTask: false,
            };
        },
        methods: {
            toggleAddTask() {
                this.showAddTask = !this.showAddTask;
            },
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

<style>
    @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
    * {
        box-sizing: border-box;
        margin: 0;
        padding: 0;
    }
    body {
        font-family: 'Poppins', sans-serif;
    }
    .container {
        max-width: 500px;
        margin: 30px auto;
        overflow: auto;
        min-height: 300px;
        border: 1px solid steelblue;
        padding: 30px;
        border-radius: 5px;
    }
    .btn {
        display: inline-block;
        background: #000;
        color: #fff;
        border: none;
        padding: 10px 20px;
        margin: 5px;
        border-radius: 5px;
        cursor: pointer;
        text-decoration: none;
        font-size: 15px;
        font-family: inherit;
    }
    .btn:focus {
        outline: none;
    }
    .btn:active {
        transform: scale(0.98);
    }
    .btn-block {
        display: block;
        width: 100%;
    }
</style>
