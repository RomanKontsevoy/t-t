<template>
    <div class="row">
        <ExcelCell
                v-for="cell in currentCellsRange"
                :key="cell.id"
                v-bind:cell="cell"/>
    </div>
</template>

<script>

    import ExcelCell from './ExcelCell';

    export default {
        name: "ExcelRow",
        components: {
            ExcelCell
        },
        props: {
            row: Number
        },
        data: function () {
            return {
                dataRow: this.row
            }
        },
        computed: {
            dataColsNum() {
                return this.$store.getters.colsNum;
            },
            dataRowsNum() {
                return this.$store.getters.rowsNum;
            },
            dataCells() {
                return this.$store.getters.cells;
            },
            currentCellsRange: function () {
                let cellsRange = this.dataCells;
                let firstIndex = this.dataRow * this.dataColsNum - this.dataColsNum;
                let lastIndex = cellsRange[this.dataRow * this.dataColsNum] ? cellsRange[this.dataRow * this.dataColsNum].id : "";
                cellsRange = lastIndex !== "" ? cellsRange.slice(firstIndex, lastIndex) : cellsRange.slice(firstIndex);
                return cellsRange;
            },
        },
        methods: {
            consoleInput: function () {
            }
        },
        mounted: function () {
            this.$nextTick(function () {
                // this.consoleInput();
            })
        }
    }
</script>

<style scoped>
    .row {
        display: flex;
        width: 298px;
    }
</style>