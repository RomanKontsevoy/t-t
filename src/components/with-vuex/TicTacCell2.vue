<template>
    <div class="cell" :class="activeClass" @click="clickHandle"> {{ content }}</div>
</template>

<script>
    export default {
        name: "TicTacCell2",
        props: {
            content: String,
            id: Number
        },
        data: function () {
            return {
                currentId: this.id
            }
        },
        computed: {
            isWinner() {
                return this.$store.getters.isWinner;
            },
            activeClass() {
                if (this.content) {
                    return {
                        "x-class" : this.content === "X",
                        "o-class" : this.content === "O"
                    }
                }
            }
        },
        methods: {
            clickHandle: function () {
                if (!this.isWinner) {
                    this.$store.dispatch('fillCell', this.currentId);
                    this.consoleClass();
                }
            },
            consoleClass: function () {
                console.log(this.activeClass);
            }
        },

        mounted: function () {
            this.$nextTick(function () {
                this.consoleClass();
            })
        }
    }
</script>

<style scoped>
    .cell {
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 40px;
        width: 80px;
        height: 80px;
        border: 1px solid rebeccapurple;
        font-family: sans-serif;
        margin: -1px 0 0 -1px;
        cursor: pointer;
    }
    .cell:hover {
        box-shadow: inset 0 0 0 1px purple;
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