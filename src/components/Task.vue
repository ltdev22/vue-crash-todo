<template>
    <div :class="[task.reminder ? 'reminder' : '', 'task']">
        <h3>{{ task.text }} <a @click="onDelete(task.id)" class="del">x</a></h3>
        <p>{{ task.day }}</p>
    </div>
</template>

<script>
    export default {
        name: 'Task',
        props: {
            task: Object,
        },
        methods: {
            onDelete(taskId) {
                this.$emit('delete-task', taskId);
            },
        },
    };
</script>

<style scope>
    .task {
        background: #f4f4f4;
        margin: 5px;
        padding: 10px 20px;
        cursor: pointer;
    }
    .task.reminder {
        border-left: 5px solid green;
    }
    .task h3 {
        display: flex;
        align-items: center;
        justify-content: space-between;
    }
</style>
