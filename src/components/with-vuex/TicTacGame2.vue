<template>
    <div class="game-wrap">
        <TicTacTable2/>
        <GameInfo2/>
    </div>

</template>

<script>
    import TicTacRow2 from './TicTacRow2';
    import TicTacTable2 from './TicTacTable2';
    import GameInfo2 from './GameInfo2';

    import Vue from 'vue';
    import Vuex from 'vuex';
    import { FILL_CELL, CREATE_CELLS, NEXT_STEP_CHECK, CALCULATE_WINNER } from '../mutation-tipes'
    Vue.use(Vuex);

    const store = new Vuex.Store({
        state: {
            colsNum: 3,
            rowsNum: 3,
            nextX: true,
            nextStep: 1,
            isWinner: null,
            cells: []
        },
        getters: {
            cells (state) {
                return state.cells
            },
            colsNum (state) {
                return state.colsNum
            },
            rowsNum (state) {
                return state.rowsNum
            },
            nextPlayer: state => {
                return state.nextX ? "X" : "O";
            },
            nextX (state) {
                return state.nextX
            },
            nextStep (state) {
                return state.nextStep
            },
            isWinner (state){
                return state.isWinner
            }
        },
        actions: {
            fillCell ({commit}, id) {
                commit (FILL_CELL, id);
                commit (NEXT_STEP_CHECK);
                commit (CALCULATE_WINNER, );
            },
            createCells ({commit}) {
                commit (CREATE_CELLS);
            }
        },
        mutations: {
            CREATE_CELLS (state) {
                let arr = new Array(state.colsNum * state.rowsNum);
                for (let i = 0; i < arr.length; i++) {
                    arr[i] = {
                        id: i,
                        content: ""
                    };
                }
                state.cells = arr;
                state.isWinner = null;
                state.nextStep = 1;
                state.nextX = true;
            },
            NEXT_STEP_CHECK (state) {
                state.nextStep++;
            },
            FILL_CELL (state, id) {
                if (state.cells[id].content === "") {
                    state.nextX ? Vue.set(state.cells[id], 'content', "X") : Vue.set(state.cells[id], 'content', "O");
                    state.nextX = !state.nextX;
                }
            },
            CALCULATE_WINNER (state) {
                let inputSquares = state.cells;
                let squares = new Array(state.colsNum * state.rowsNum).fill(null);
                for (let i = 0; i < squares.length; i++) {
                    if (inputSquares[i].content !== "") squares[i] = inputSquares[i].content;
                }
                const lines = [
                    [0, 1, 2],
                    [3, 4, 5],
                    [6, 7, 8],
                    [0, 3, 6],
                    [1, 4, 7],
                    [2, 5, 8],
                    [0, 4, 8],
                    [2, 4, 6],
                ];
                for (let i = 0; i < lines.length; i++) {
                    const [a, b, c] = lines[i];
                    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
                        state.isWinner = squares[a];
                    }
                }
                return null;
            }
        }
    });

    export default {
        store,
        name: "TicTacGame2",
        components: {
            TicTacRow2,
            TicTacTable2,
            GameInfo2
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
        mounted: function () {
            this.$nextTick(function () {
                this.$store.dispatch('createCells');
            })
        }
    }
</script>

<style scoped>

</style>