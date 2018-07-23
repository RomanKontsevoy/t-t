<template>
    <div class="row">
        <TicTacCell2
                v-for="cell in currentCellsRange"
                :key="cell.id"
                v-bind="cell" />
    </div>
</template>

<script>

    import TicTacCell2 from './TicTacCell2.vue';

    export default {
        name: "TicTacRow2",
        components: {
            TicTacCell2
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
            }
        },
        mounted: function () {
            this.$nextTick(function () {
                // console.log(this._props.row);
            })
        }
    }
</script>

<style scoped>
    .row {
        display: flex;
        width: 238px;
    }

</style>