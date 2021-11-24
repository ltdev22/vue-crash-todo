<template>
    <header>
        <h1>{{ appTitle }}</h1>
        <Button
            @btn-click="$emit('toggle-add-task')"
            :btnColor="showAddTask ? 'red' : 'green'"
            :btnText="showAddTask ? 'Close' : 'Add'"
        />
    </header>
</template>

<script>
    import Button from './Button';
    export default {
        name: 'Header',
        props: {
            appTitle: {
                type: String,
                default: 'Hello Vue',
            },
            showAddTask: Boolean,
        },
        components: {
            Button,
        },
    };
</script>

<style scoped>
    header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 20px;
    }
</style>
