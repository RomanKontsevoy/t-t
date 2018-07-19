<template>
    <div class="table">
        <TicTacRow
                v-for="row in rowsNum"
                v-bind:colsNum="colsNum"
                v-bind:rowsNum="rowsNum"
                v-bind:cells="cells"
                v-bind:row="row"
                @click-cell="cellClickHandle"/>

    </div>
</template>

<script>
    import TicTacRow from './TicTacRow';

    export default {
        name: "TicTacTable",
        components: {
            TicTacRow
        },
        props: {
            colsNum: Number,
            rowsNum: Number,
            cells: Array,
        },
        data: function () {
            return {

            }
        },
        methods: {
            cellClickHandle: function (id) {
                this.$emit('click-cell', id);
            }
        },
    }
</script>

<style scoped>
    .table {
        display: flex;
        width: 118px;
        flex-wrap: wrap;
        margin: 30px auto 0;
    }

</style>