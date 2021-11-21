<template>
    <button @click="onClick()" :style="{ background: btnColor }" class="btn">{{ btnText }}</button>
</template>

<script>
export default {
    name: 'Button',
    props: {
        btnText: String,
        btnColor: String
    },
    methods: {
        onClick() {
            console.log('Click!');
        }
    }
}
</script>