<template>
    <div class="table">
        <ExcelRow
                v-for="row in rowsNum"
                v-bind:row="row"/>
    </div>
</template>

<script>
    import ExcelRow from './ExcelRow';

    export default {
        name: "ExcelTable",
        components: {
            ExcelRow
        },
        data: function () {
            return {

            }
        },
        computed: {
            rowsNum() {
                return this.$store.getters.rowsNum;
            }
        },
    }
</script>

<style scoped>
    .table {
        display: flex;
        flex-wrap: wrap;
        width: 298px;
        margin: 30px auto 0;
    }
</style>