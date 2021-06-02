<template>
  <div class="game">
      <div class="game__result"></div>

      <div class="game__field">
        <div class="game__element"></div>
        <div class="game__element"></div>
        <div class="game__element"></div>
        <div class="game__element"></div>
        <div class="game__element"></div>
        <div class="game__element"></div>
        <div class="game__element"></div>
        <div class="game__element"></div>
        <div class="game__element"></div>
      </div>

      <button class="game__btn">New game</button>
  </div>
</template>

<script>
export default {

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

        &__result{
            color: green;
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

        &__element{
            width: 120px;
            height: 120px;
            border: 2px solid black;
            cursor: pointer;
        }

        &__btn{
            padding: 10px 15px;
            cursor: pointer;
            border-radius: 5px;
            font-size: 25px;
        }
    }

    .active{
        background: rgba(0, 0, 0, 0.3);
    }
</style>