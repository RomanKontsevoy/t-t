<template>
    <div class="cell">
        <textarea
                ref="textarea"
                type="text"
               :class="{'active': activeClass}"
                @click="activate"
                v-model="currentCell.content"
                v-bind:cols="cols">
        </textarea>
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
                cols: 10,
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
        watch: {
            'currentCell.content': function (newVal, oldVal) {
                console.log('value changed from ' + oldVal + ' to ' + newVal);
                this.colsHandle();
            }
        },
        methods: {
            colsHandle: function() {
                let textlength = this.$refs.textarea.textLength;
                if(textlength <= 10) {
                    console.log(textlength);
                    this.cols = 10;
                } else if (textlength > 30) {
                    console.log(textlength);
                    this.cols = 30;
                } else {
                    console.log(textlength);
                    this.cols = textlength;
                }
            },
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
                console.dir(this.$refs.textarea);
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
        height: 40px;
        width: 100px;
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
        height: 100%;
        border: none;
        padding: 0 5px;
        resize: none;
    }

    .cell .active {
        display: inline-block;
        border: 1px solid saddlebrown;
        max-width: 80vw;
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