<template>
    <header>
        <h1>{{ appTitle }}</h1>
    </header>
</template>

<script>
export default {
    name: 'Header',
    props: {
        appTitle: {
            type: String,
            default: 'Hello Vue'
        }
    },
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