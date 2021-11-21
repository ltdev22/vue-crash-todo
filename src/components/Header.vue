<template>
    <header>
        <h1>{{ appTitle }}</h1>
        <Button btnText="Add Task" btnColor="green" />
    </header>
</template>

<script>
import Button from './Button'
export default {
    name: 'Header',
    props: {
        appTitle: {
            type: String,
            default: 'Hello Vue'
        }
    },
    components: {
        Button
    }
}
</script>

<style scoped>
header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
}
</style>