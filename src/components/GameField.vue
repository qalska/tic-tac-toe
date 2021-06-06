<template>
  <div class="game">
        <div class="game__message"> {{ message }} </div>

        <div class="game__field">
            <div class="game__cell"
            :class="cell.isWinClass"
            v-for="(cell, index) of cells"
            :key="cell.index"
            @click="onCellClick(index)">
                <span class="game__cell-inner">{{ cell.inner }}</span>
            </div>
        </div>

        <button class="game__btn" @click="loadNewGame()">New game</button>
  </div>
</template>

<script>
export default {
    data() {
        return {
            player: 'x',
            count: 0,
            cells: [
                {index: 1, inner: null, isWinClass: null},
                {index: 2, inner: null, isWinClass: null},
                {index: 3, inner: null, isWinClass: null},
                {index: 4, inner: null, isWinClass: null},
                {index: 5, inner: null, isWinClass: null},
                {index: 6, inner: null, isWinClass: null},
                {index: 7, inner: null, isWinClass: null},
                {index: 8, inner: null, isWinClass: null},
                {index: 9, inner: null, isWinClass: null},
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
            messages: {
                alert: 'Cell is not free!',
                crossWon: 'Crosses won!',
                zeroWon: 'Zeroes won!',
                draw: 'Draw!'
            },
            message: null
        }
    },
    methods: {
        onCellClick(index) {
            let cell = this.cells[index];

            // Заполняем клетки ходами X или 0, предупреждаем о двойном нажатии на занятую клетку
            if (cell.inner == null) {
                cell.inner = this.player;
            } else {
                this.message = this.messages.alert;
                return
            }

            this.player = this.player == 'x' ? '0' : 'x';

            // Считаем ходы и убираем предупреждение
            this.count++

            this.message = null;

            this.getWinner()
        },

        loadNewGame() {

        },

        getWinner() {
            // Проходимся по массиву выигрышных индексов и проверяем на совпадения
            this.winningIndex.forEach( (i) => {
                if (this.cells[(i[0] - 1)].inner == 'x' &&
                this.cells[(i[1] - 1)].inner == 'x' &&
                this.cells[(i[2] - 1)].inner == 'x') {
                    this.message = this.messages.crossWon;
                    this.cells[(i[0] - 1)].isWinClass = 'is-win'
                    this.cells[(i[1] - 1)].isWinClass = 'is-win'
                    this.cells[(i[2] - 1)].isWinClass = 'is-win'
                }

                else if (this.cells[(i[0] - 1)].inner == '0' &&
                this.cells[(i[1] - 1)].inner == '0' &&
                this.cells[(i[2] - 1)].inner == '0') {
                    this.message = this.messages.zeroWon;
                    this.cells[(i[0] - 1)].isWinClass = 'is-win'
                    this.cells[(i[1] - 1)].isWinClass = 'is-win'
                    this.cells[(i[2] - 1)].isWinClass = 'is-win'
                }

                // Ничья, если все клетки заняты
                else if (this.count == 9) {
                    this.message = this.messages.draw;
                }
            })           
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
            color: #be1d1d;
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

    .is-win{
        background-color: rgba(53, 170, 29, 0.75);
        &:hover{
            background-color: rgba(53, 170, 29, 0.75);
        }
    }
</style>