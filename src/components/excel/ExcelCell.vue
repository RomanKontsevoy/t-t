<template>
    <div class="cell">
        <vue-draggable-resizable :w="100" :h="100" v-on:dragging="onDrag" v-on:resizing="onResize" :parent="true">
        <textarea
                type="text"
               :class="{'active': activeClass}"
                @click="activate"
                v-model="currentCell.content" />
        </vue-draggable-resizable>
    </div>

</template>

<script>
    import Vue from 'vue'
    import VueDraggableResizable from 'vue-draggable-resizable'

    Vue.component('vue-draggable-resizable', VueDraggableResizable)



    export default {
        name: "ExcelCell",
        props: {
            cell: Object
        },
        data: function () {
            return {
                currentCell: this.cell,
                width: 0,
                height: 0,
                x: 0,
                y: 0
            }
        },
        computed: {
            activated () {
                return this.$store.getters.activeId
            },
            activeClass () {
                return !!this.currentCell.isActive // this.activated ? true :false
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
        position: relative;
        overflow: visible;
    }

    .cell:hover {
        box-shadow: inset 0 0 2px purple;
    }

    .cell textarea {
        display: block;
        width: 100%;
        height: 100%;
        border: none;
        padding: 0 5px;
        resize: none;
    }

    .cell .active {
        display: inline-block;
        border: 1px solid saddlebrown;
        max-width: 80vw;
        width: auto;
        resize: both;
        left: 50%;
        transform: translateX(-50%);
        position: absolute;
        z-index: 5;
        box-sizing: content-box;
        height: content-box;
    }

    .o-class {
        color: yellow;
        background-color: rgba(0, 150, 136, 0.5);
    }
</style>