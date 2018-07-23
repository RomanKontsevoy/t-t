<template>
    <div class="table">
        <TicTacRow2
                v-for="row in rowsNum"
                v-bind:row="row"/>
    </div>
</template>

<script>
    import TicTacRow2 from './TicTacRow2';
    export default {
        name: "TicTacTable2",
        components: {
            TicTacRow2
        },
        data: function () {
            return {

            }
        },
        computed: {
            rowsNum() {
                return this.$store.getters.rowsNum;
            },
        },
    }
</script>

<style scoped>
    .table {
        display: flex;
        width: 238px;
        flex-wrap: wrap;
        margin: 30px auto 0;
    }
</style>