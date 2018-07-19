<template>
    <div class="game-wrap">
        <TicTacTable
                v-bind:colsNum="colsNum"
                v-bind:rowsNum="rowsNum"
                v-bind:cells="cells"
                @click-cell="fillCell"/>
        <GameInfo
                v-bind:nextPlayer="nextPlayer"
                v-bind:nextStep="nextStep"
                v-bind:isWinner="isWinner"/>

    </div>
</template>

<script>
    import TicTacTable from './TicTacTable';
    import GameInfo from './GameInfo';

    export default {
        name: "TicTacGame",
        components: {
            TicTacTable,
            GameInfo
        },
        data: function () {
            return {
                colsNum: 3,
                rowsNum: 3,
                nextX: true,
                nextStep: 1,
                isWinner: null
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
            },
            nextPlayer: function () {
                return this.nextX ? "X" : "O";
            }
        },
        methods: {
            nextStepCheck: function () {
                return this.nextStep++;
            },
            fillCell: function (id) {
                if (this.cells[id].content === "") {
                    this.nextX ? this.$set(this.cells[id], 'content', "X") : this.$set(this.cells[id], 'content', "O");
                    this.nextX = !this.nextX;
                    this.nextStepCheck();
                    if (this.calculateWinner(this.cells)) {
                        this.isWinner = this.calculateWinner(this.cells);
                    }
                }
            },
            calculateWinner: function (inputSquares) {
                let squares = new Array(this.colsNum * this.rowsNum).fill(null);
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
                        return squares[a];
                    }
                }
                return null;
            }
        }
    }
</script>

<style scoped>

</style>