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
            player: 'X',
            count: 0,
            inProgress: true,
            cells: [
                {inner: null, isWinClass: null},
                {inner: null, isWinClass: null},
                {inner: null, isWinClass: null},
                {inner: null, isWinClass: null},
                {inner: null, isWinClass: null},
                {inner: null, isWinClass: null},
                {inner: null, isWinClass: null},
                {inner: null, isWinClass: null},
                {inner: null, isWinClass: null},
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
            messages: {
                alert: 'Cell is not free!',
                'X': 'Crosses won!',
                'O': 'Zeroes won!',
                draw: 'Draw!'
            },
            message: null
        }
    },
    methods: {
        onCellClick(index) {
            let cell = this.cells[index];

            // Заполняем клетки ходами X или 0, предупреждаем о двойном нажатии на занятую клетку
            if (this.inProgress && cell.inner === null) {
                cell.inner = this.player;
                this.player = this.player == 'X' ? 'O' : 'X';
                this.setMessage(null)
            } 
            else if (cell.inner === null) {
                this.setMessage(this.messages);
            } else {
                this.setMessage(this.messages.alert);
                return
            }

            // Считаем ходы
            this.count++

            this.getWinner();
        },

        getWinner() {
            this.winningIndex.forEach( (i) => {
                const [idx1, idx2, idx3] = i;
                const cellIdx1 = this.cells[(idx1 - 1)],
                      cellIdx2 = this.cells[(idx2 - 1)],
                      cellIdx3 = this.cells[(idx3 - 1)];

                if (cellIdx1.inner &&
                    cellIdx1.inner === cellIdx2.inner &&
                    cellIdx1.inner === cellIdx3.inner) {
                    cellIdx1.isWinClass = cellIdx2.isWinClass = cellIdx3.isWinClass = 'is-win';
                    this.setMessage(this.messages[cellIdx1.inner]);
                    this.dropProgress();
                    this.dropCount();
                }

                // Ничья, если все клетки заняты
                else if (this.count === 9) {
                    this.setMessage(this.messages.draw);
                    this.dropProgress();
                    this.dropCount();
                }
            })           
        },
        loadNewGame() {
            //Обнуляем все значения
            this.setMessage(null);
            this.inProgress = true;

            this.cells.forEach( (currentCell) => {
                currentCell.inner = null;
                currentCell.isWinClass = null;
            })
        },

        setMessage(message) {
            this.message = message;
        },

        dropProgress() {
            this.inProgress = false;
        },

        dropCount() {
            this.count = 0;
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