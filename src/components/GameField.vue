<template>
  <div class="game">
        <div class="game__message"></div>

        <div class="game__field">
            <div class="game__cell" 
            v-for="(cell, index) of cells"
            :key="cell.index"
            @click="onCellClick(index)">
                <!-- <img :src="cell.imageUrl"> -->
                <span class="game__cell-inner">{{cell.inner}}</span>
            </div>
        </div>

        <button class="game__btn" @click="loadNewGame()">New game</button>
  </div>
</template>

<script>
export default {
    data() {
        return {
            step: false,
            isShow: false,
            // players: [
            //     {
            //         name: 'cross',
            //         playerImage: './assets/cross.svg'
            //     },
            //     {
            //         name: 'zero',
            //         playerImage: './assets/zero.svg'
            //     }
            // ],
            player: 'x',
            cells: [
                {index: 1, inner: null},
                {index: 2, inner: null},
                {index: 3, inner: null},
                {index: 4, inner: null},
                {index: 5, inner: null},
                {index: 6, inner: null},
                {index: 7, inner: null},
                {index: 8, inner: null},
                {index: 9, inner: null},
            ],
            winningIndex: [
                [1, 2 ,3],
                [4, 5, 6],
                [7, 8, 9],
                [1, 4, 7],
                [2, 5, 8],
                [3, 6, 9],
                [1, 5, 9],
                [3, 5, 7]
            ],
            data: [],
            messages: []
        }
    },
    methods: {
        onCellClick(index) {
            let cell = this.cells[index];
            if (cell.inner == null) {
                cell.inner = this.player
            } else {
                this.isShow = true 
            }

            this.isShow = false
        },
        loadNewGame() {

        },

        getWinner() {

        }
    },
}
</script>

<style lang="scss" scoped>
    *{
        box-sizing: border-box;
    }
    .game {
        display: flex;
        align-items: center;
        justify-content: center;
        flex-direction: column;

        &__message{
            color: #9c2222;
            font-size: 35px;
            font-weight: bolder;
            margin-top: 20px;
            height: 35px;
        }

        &__field{
            width: 360px;
            height: 360px;
            display: flex;
            flex-wrap: wrap;
            outline: 3px solid black;
            margin: 80px 0 50px 0;
        }

        &__cell{
            width: 120px;
            height: 120px;
            border: 2px solid black;
            cursor: pointer;
            text-align: center;
            &:hover{
                background: #F1F1F1;
            }
            &-inner{
                font-size: 100px;
            }
        }

        &__btn{
            padding: 10px 15px;
            cursor: pointer;
            border-radius: 5px;
            font-size: 25px;
        }
    }

    // .active{
    //     background: rgba(0, 0, 0, 0.3);
    // }
</style>