<template>
    <div class="game-info">
        <div v-if="!isWinner">
            <h3>Next player is: {{nextPlayer}}</h3>
            <p>Current step: {{nextStep}}</p>
        </div>
        <h2 v-else>The winner is: {{isWinner}}!!!</h2>
    </div>
</template>

<script>
    export default {
        name: "GameInfo",
        props: {
            nextPlayer: String,
            nextStep: Number,
            isWinner: String
        },
        data: function () {
            return {}
        },
        methods: {
            clickHandle: function () {
                this.$emit('click-cell', this.id);
            }
        }
    }
</script>

<style scoped>
    .game-info {
        margin-top: 20px;
    }
</style>