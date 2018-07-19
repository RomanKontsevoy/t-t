<template>
    <div class="table">
        <TicTacRow
                v-for="row in rowsNum"
                v-bind:colsNum="colsNum"
                v-bind:rowsNum="rowsNum"
                v-bind:cells="cells"
                v-bind:row="row"
                @click-cell="fillCell"/>

    </div>
</template>

<script>
    import TicTacRow from './TicTacRow';

    export default {
        name: "TicTacTable",
        components: {
            TicTacRow
        },

        data: function () {
            return {
                colsNum: 3,
                rowsNum: 3
            }
        },
        computed: {
            cells: {
                // геттер:
                get: function () {
                    let arr = new Array(this.colsNum * this.rowsNum);
                    for (let i = 0; i < arr.length; i++) {
                        arr[i] = {
                            id: i,
                            content: ""
                        };
                    }
                    return arr;
                },
                // сеттер:
                set: function (id, newValue) {
                    this.cells[id].content = newValue;
                }
            }
        },
        methods: {
            fillCell: function (id) {
                this.cells[id].content === "" ? this.$set(this.cells[id], 'content', "X") : this.$set(this.cells[id], 'content', "");
                // this.$set(this.someObject, 'b', 2);
                // Vue.set(object, key, value);
                this.consoleLog(id);
            },
            consoleLog: function (id) {
                // console.log(this.cells[id].content);
                console.log(this._computedWatchers.cells.value[id].content);
            }
        },
        mounted: function () {
            this.$nextTick(function () {
                // console.log(this.cells[0].content);
            })
        }
    }
</script>

<style scoped>
    .table {
        display: flex;
        width: 118px;
        flex-wrap: wrap;
        margin: 30px auto 0;
    }

</style>