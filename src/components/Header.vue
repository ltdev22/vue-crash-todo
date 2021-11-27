<template>
    <header>
        <h1>{{ appTitle }}</h1>
        <Button
            v-show="isHomePage"
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
        computed: {
            isHomePage() {
                if (this.$route.path === '/') {
                    return true;
                } else {
                    return false;
                }
            },
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
