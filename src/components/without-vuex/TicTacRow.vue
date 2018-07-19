<template>
    <div class="row">
        <TicTacCell
                v-for="cell in currentCellsRange"
                :key="cell.id"
                v-bind="cell"
                @click-cell="cellClickHandle"/>
    </div>
</template>

<script>

    import TicTacCell from './TicTacCell.vue';

    export default {
        name: "TicTacRow",
        components: {
            TicTacCell
        },
        props: {
            colsNum: Number,
            rowsNum: Number,
            cells: Array,
            row: Number
        },
        data: function () {
            return {
                dataColsNum: this.colsNum,
                dataRowsNum: this.rowsNum,
                dataCells: this.cells,
                dataRow: this.row
            }
        },
        computed: {
            currentCellsRange: function () {
                let cellsRange = this.dataCells;
                let firstIndex = this.dataRow * this.dataColsNum - this.dataColsNum;
                let lastIndex = cellsRange[this.dataRow * this.dataColsNum] ? cellsRange[this.dataRow * this.dataColsNum].id : "";
                cellsRange = lastIndex !== "" ? cellsRange.slice(firstIndex, lastIndex) : cellsRange.slice(firstIndex);
                return cellsRange;
            }
        },
        methods: {
            cellClickHandle: function (id) {
                this.$emit('click-cell', id);
            }
        }
    }
</script>

<style scoped>
    .row {
        display: flex;
        width: 118px;
    }

</style>