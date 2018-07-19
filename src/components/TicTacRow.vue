<template>
    <div class="row">
        <TicTacCell
                v-for="cell in currentCellsRange"
                :key="cell.id"
                v-bind:cell="cell"
                @click-cell="consoleId"/>
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
            return {}
        },
        computed: {
            currentCellsRange: function () {
                let cellsRange = this.cells;
                let firstIndex = this.row * this.colsNum - this.colsNum;
                let lastIndex = cellsRange[this.row * this.colsNum] ? cellsRange[this.row * this.colsNum].id : "";
                cellsRange = lastIndex !== "" ? cellsRange.slice(firstIndex, lastIndex) : cellsRange.slice(firstIndex);
                return cellsRange;
            }
        },
        methods: {
            consoleId: function (id) {
                // console.log(id);
                this.$emit('click-cell', id);
            }
        },
        mounted: function () {
            this.$nextTick(function () {
            })
        }
    }
</script>

<style scoped>
    .row {
        display: flex;
        width: 118px;
    }

</style>