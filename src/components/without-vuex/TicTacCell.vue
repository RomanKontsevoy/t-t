<template>
    <div class="cell" @click="clickHandle"> {{ content }}</div>
</template>

<script>
    export default {
        name: "TicTacCell",
        props: {
            content: String,
            id: Number
        },
        data: function () {
            return {}
        },
        methods: {
            clickHandle: function () {
                this.$emit('click-cell', this.id);
            }
        }
    }
</script>

<style scoped>
    .cell {
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 20px;
        width: 40px;
        height: 40px;
        border: 1px solid rebeccapurple;
        font-family: sans-serif;
        margin: -1px 0 0 -1px;
        cursor: pointer;

    }

    .cell:hover {
        background: #f0f0f0;
    }
</style>