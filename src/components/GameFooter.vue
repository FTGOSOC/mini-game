<template>
        <div class="gameFooter">
      <span class="user">Гравець {{ userScore }}</span> / <span class="pc">{{ pcScore }} Комп'ютер</span>
    </div>
</template>

<script>
    export default {
        name: 'GameFooter',
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

  .gameFooter {
    width: 596px;
    padding: 10px;
    text-align: center;
  }

  .user {
    color: #73FFA1;
  }

  .pc {
    color: #E02C2C;
  }
</style>