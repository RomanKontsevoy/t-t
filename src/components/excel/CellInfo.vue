<template>
    <div class="game-info">
        <div v-if="!isWinner">
            <h3>Next player is: {{nextPlayer}}</h3>
            <p>Current step: {{nextStep}}</p>
        </div>
        <h2 class="winner" v-else>The winner is: <span :class="winnerClass">{{isWinner}}</span>!!!</h2>
        <button class="reset" :class="{ active: resetActive }" @click="resetGame">Reset game</button>
    </div>
</template>

<script>
    export default {
        name: "CellInfo",
        data: function () {
            return {

            }
        },
        computed: {
            nextPlayer() {
                return this.$store.getters.nextPlayer;
            },
            nextStep() {
                return this.$store.getters.nextStep;
            },
            isWinner() {
                return this.$store.getters.isWinner;
            },
            resetActive() {
                return !!this.$store.getters.isWinner;
            },
            winnerClass() {
                if (this.isWinner) {
                    return {
                        "x-class" : this.isWinner === "X",
                        "o-class" : this.isWinner === "O"
                    }
                }
            }
        },
        methods: {
            resetGame: function () {
                this.$store.dispatch('createCells');
            }
        }
    }
</script>

<style scoped>
    .game-info {
        margin-top: 20px;
    }
    .reset {
        margin: 20px 10px;
        display: inline-block;
        padding: 10px;
        background: #41b883;
        opacity: .6;
        text-decoration: none;
        text-transform: uppercase;
        color: #fff;
        border: none;
        cursor: pointer;
    }
    .reset:hover {
        opacity: 1;
    }
    .winner {
        max-width: 300px;
        text-align: center;
        margin: auto;
    }
    .active {
        transform: scale(1.5) translateY(25%);
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