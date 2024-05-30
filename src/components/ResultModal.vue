<template>
        <div class="resultsModalWrap" @click="$emit('close')">
      <div class="resultsModal">
        Рахунок
        <br>
        <span class="user">Гравець {{ userScore }}</span> / <span class="pc">{{ pcScore }} Комп'ютер</span>
      </div>
    </div>
</template>

<script>
    export default {
        name: 'ResultModal',
        props: {
            userScore: {
                type: Number,
                default: 0,
            },
            pcScore: {
                type: Number,
                default: 0,
            }
        }
    }
</script>

<style lang="scss" scoped>

.resultsModalWrap {
    position: absolute;
    height: 100vh;
    width: 100vw;
    left: 0;
    top: 0;
    background-color: rgba(255, 255, 255, .2);
    backdrop-filter: blur(2px);
    display: flex;
    justify-content: center;
    align-items: center;

    .resultsModal {
      color: #fff;
      background-color: #0C0D11;
      border-radius: 20px;
      padding: 20px;
      text-align: center;
    }
  }

  .user {
    color: #73FFA1;
  }

  .pc {
    color: #E02C2C;
  }
</style>
