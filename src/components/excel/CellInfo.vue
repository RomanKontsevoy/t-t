<template>
    <div class="game-info">
        <div v-if="activated">
            <p>ID ячейки: {{currentCell.id}}</p>
            <p>Номер строки: {{currentCell.rowNum}}</p>
            <p>Номер столбца: {{currentCell.colNum}}</p>
            <label for="currentContent">
                <input id="currentContent" type="text" v-model="currentCell.content">
            </label>
        </div>
        <div @click="consoleInput" class="no-cell" v-else>Ни одна ячейка не выбрана</div>
    </div>
</template>

<script>
    export default {
        name: "CellInfo",
        data: function () {
            return {}
        },
        computed: {
            cells() {
                return this.$store.getters.cells;
            },
            activated() {
                return this.$store.getters.activeCell;
            },
            active() {
                return this.$store.getters.activeId;
            },
            currentCell() {
                return this.cells[this.active];
            },
        },
        methods: {
            consoleInput: function () {
                // if (this.activated) {
                //     console.dir("ID ячейки: " + this.currentCell.id);
                //     console.dir("Есть активная: " + this.activated)
                // }
                // console.dir("ID ячейки: " + this.currentCell.id);
                // console.dir("Активность ячейки: " + this.currentCell.isActive);
                // console.log(this.currentCells);
                // console.log("Столбец: " + this.currentCell.colNum);
                // console.log("Активность: " + this.currentCell.isActive);
            }
        },
        mounted: function () {
            this.$nextTick(function () {
                // this.consoleInput();
            })
        },
    }
</script>

<style scoped>
    .game-info {
        margin-top: 20px;
    }
    .no-cell {
        cursor: pointer;
    }
</style>