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
    import {FILL_CELL, CREATE_CELLS, ACTIVATE_CELL} from '../mutation-tipes'

    Vue.use(Vuex);

    const store = new Vuex.Store({
        state: {
            colsNum: 3,
            rowsNum: 2,
            cells: [],
            activeId: "",
            activeCell: false
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
            },
            activeId(state) {
                return state.activeId
            },
            activeCell(state) {
                return state.activeCell
            }
        },
        actions: {
            fillCell({commit}, id, text) {
                commit(FILL_CELL, id, text);
            },
            activateCell({commit}, id) {
                commit(ACTIVATE_CELL, id);
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
                        rowNum: Math.floor(i / state.colsNum),
                        content: "",
                        isActive: false
                    };
                }
                state.cells = arr;
            },
            FILL_CELL(state, id, text) {
                Vue.set(state.cells[id], 'content', text);
            },
            ACTIVATE_CELL(state, id) {
                /*1*/
                // for (let i = 0; i < state.cells.length; i++ ) {
                //     if(state.cells[i].isActive) {
                //         console.log(state.cells[i].isActive);
                //         Vue.set(state.cells[i].isActive, 'isActive', false)
                //     }
                // }
                /*2*/
                // state.cells.forEach(function (item) {
                //    if(item.isActive) {
                //        Vue.set(item.isActive, 'isActive', false)
                //    }
                // });
                /*3*/
                // Vue.set(state.cells.find(item => item.isActive), 'isActive', false);

                Vue.set(state.cells[id], 'isActive', true);
                state.activeCell = true;
                state.activeId = id;
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
                        console.log("item.colNum: " + item.colNum);
                        console.log("item.rowNum: " + item.rowNum);
                    }
                );
            }
        },
        mounted: function () {
            this.$nextTick(function () {
                this.$store.dispatch('createCells');
                // this.consoleInput();
            })
        }
    }
</script>

<style scoped>

</style>