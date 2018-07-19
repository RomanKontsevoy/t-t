<template>
    <div class="cell" @click="$emit('click-cell', cell.id)"> {{ cell.content }} </div>
</template>

<script>
    export default {
        name: "TicTacCell",
        props: {
          cell: Object
        },
        data: function () {
            return {

            }
        },
        mounted: function () {
            this.$nextTick(function () {
                // console.log(this.cell.id);
                // console.log(this.cell.content);
            })
        }
    }
</script>

<style scoped>
    .cell {
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 20px;
        width: 40px;
        height: 40px;
        border: 1px solid rebeccapurple;
        font-family: sans-serif;
        margin: -1px 0 0 -1px;
        cursor: pointer;

    }
    .cell:hover {
         background: #f0f0f0;
     }
</style>