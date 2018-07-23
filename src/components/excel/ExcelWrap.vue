<template>
    <div class="game-wrap">
        <ExcelTable/>
        <CellInfo/>
    </div>

</template>

<script>
    import ExcelTable from './ExcelTable';
    import CellInfo from './CellInfo';

    import Vue from 'vue';
    import Vuex from 'vuex';
    import {FILL_CELL, CREATE_CELLS} from '../mutation-tipes'

    Vue.use(Vuex);

    const store = new Vuex.Store({
        state: {
            colsNum: 3,
            rowsNum: 2,
            cells: []
        },
        getters: {
            cells(state) {
                return state.cells
            },
            colsNum(state) {
                return state.colsNum
            },
            rowsNum(state) {
                return state.rowsNum
            }
        },
        actions: {
            fillCell({commit}, id, text) {
                commit(FILL_CELL, id, text);
            },
            createCells({commit}) {
                commit(CREATE_CELLS);
            }
        },
        mutations: {
            CREATE_CELLS(state) {
                let totalCellsNum = state.colsNum * state.rowsNum;
                let arr = new Array(totalCellsNum);
                for (let i = 0; i < arr.length; i++) {
                    arr[i] = {
                        id: i,
                        colNum: i % state.colsNum,
                        rowNum: parseInt(i % state.colsNum, 10) % state.rowsNum,
                        content: "",
                        isActive: false
                    };
                }
                state.cells = arr;
            },
            FILL_CELL(state, id, text) {
                Vue.set(state.cells[id], 'content', text);
                state.cells.forEach(function (item) {
                        Vue.set(item, 'isActive', false);
                    }
                );
                Vue.set(state.cells[id], 'isActive', true);
            }
        }
    });

    export default {
        store,
        name: "ExcelWrap",
        components: {
            ExcelTable,
            CellInfo
        },
        computed: {
            cells() {
                return this.$store.getters.cells;
            },
            colsNum() {
                return this.$store.getters.colsNum;
            },
            rowsNum() {
                return this.$store.getters.rowsNum;
            }
        },
        methods: {
            consoleInput: function () {
                this.cells.forEach(function (item) {
                        console.log("item.Id: " + item.id);
                        // console.log("item.colNum: " + item.colNum);
                        console.log("item.rowNum: " + item.rowNum);

                    }
                );
            }
        },
        mounted: function () {
            this.$nextTick(function () {
                this.$store.dispatch('createCells');
                this.consoleInput();
            })
        },
        updated: function () {
            this.$nextTick(function () {
                this.consoleInput();
            })
        }
    }
</script>

<style scoped>

</style>