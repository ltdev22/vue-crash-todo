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
    </div>
</template>

<script>
    import Header from './components/Header';
    import Tasks from './components/Tasks';
    import AddTask from './components/AddTask';

    export default {
        name: 'App',
        components: {
            Header,
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
            addTask(newTask) {
                this.tasks = [...this.tasks, newTask];
            },
            deleteTask(taskId) {
                this.tasks = this.tasks.filter((task) => {
                    return task.id !== taskId;
                });
            },
            toggleReminder(taskId) {
                this.tasks = this.tasks.map((task) => {
                    return task.id == taskId ? { ...task, reminder: !task.reminder } : task;
                });
            },
        },
        created() {
            this.tasks = [
                {
                    id: 1,
                    text: 'Book flight tickets',
                    day: '26th of November at 9:00pm',
                    reminder: true,
                },
                {
                    id: 2,
                    text: 'Buy Christmas gifts',
                    day: '23rd of December at 10:30am',
                    reminder: true,
                },
                {
                    id: 3,
                    text: 'Buy Christmas turkey',
                    day: '25th of December at 2:30pm',
                    reminder: false,
                },
            ];
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
