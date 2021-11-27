<template>
    <footer>
        <p>Copyright &copy; 2021</p>
        <router-link to="/">Home</router-link>
        &nbsp;&bull;&nbsp;
        <router-link to="/about">About</router-link>
    </footer>
</template>

<style scoped>
    footer {
        margin-top: 30px;
        text-align: center;
    }

    footer a {
        color: #333;
    }
</style>
