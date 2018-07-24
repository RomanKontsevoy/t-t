<template>
        <input type="text" class="cell" :class="activeClass" @click="activate" v-model="currentCell.content">
</template>

<script>
    export default {
        name: "ExcelCell",
        props: {
            cell: Object
        },
        data: function () {
            return {
                currentCell: this.cell
            }
        },
        computed: {
            activated(){
                this.$store.getters.activeId
            },
            activeClass() {

            }
        },
        methods: {
            clickHandle: function () {
                this.$store.dispatch('fillCell', this.currentCell.id, this.currentCell.content);
                // this.consoleInput();
            },
            activate: function () {
                this.$store.dispatch('activateCell', this.currentCell.id);
                this.consoleInput();
            },
            consoleInput: function () {
                console.dir("ID ячейки: " + this.currentCell.id);
                // console.log("Строка: " + this.currentCell.rowNum);
                // console.log("Столбец: " + this.currentCell.colNum);
                console.log("Активность: " + this.currentCell.isActive);
                console.log("Активная ячейка: " + this.activated);
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
    .cell {
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 30px;
        width: 100px;
        height: 40px;
        border: 1px solid rebeccapurple;
        font-family: sans-serif;
        margin: -1px 0 0 -1px;
        cursor: text;
    }

    .cell:hover {
        box-shadow: inset 0 0 2px purple;
    }

    .x-class {
        color: red;
        background-color: rgba(0, 128, 0, 0.2);
    }

    .o-class {
        color: yellow;
        background-color: rgba(0, 150, 136, 0.5);
    }
</style>