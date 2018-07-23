<template>
        <input type="text" class="cell" :class="activeClass" @input="clickHandle" v-model="currentContent">

</template>

<script>
    export default {
        name: "ExcelCell",
        props: {
            content: String,
            id: Number
        },
        data: function () {
            return {
                currentId: this.id,
                currentContent: this.content
            }
        },
        computed: {
            activeClass() {
                // if (this.content) {
                //     return {
                //         "x-class": this.currentContent === "X",
                //         "o-class": this.currentContent === "O"
                //     }
                // }
            }
        },
        methods: {
            clickHandle: function () {
                this.$store.dispatch('fillCell', this.currentId, this.currentContent);
                this.consoleInput();
            },
            consoleInput: function () {
                console.dir(this.currentContent);
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