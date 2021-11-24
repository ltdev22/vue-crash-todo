<template>
    <button @click="onClick()" :style="{ background: btnColor }" class="btn">{{ btnText }}</button>
</template>

<script>
    export default {
        name: 'Button',
        props: {
            btnText: String,
            btnColor: String,
        },
        methods: {
            onClick() {
                this.$emit('btn-click');
            },
        },
    };
</script>
