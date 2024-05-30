<template>
  <div class="theGame">
    <GameInput v-model="timer" :gameInProgress="gameInProgress" @start="startTheGame" />
    <div class="tilesWrapBg">
      <div class="tilesWrap">
        <div class="tiles">
          <div class="tileItem" v-for="(tile, index) in tiles" :key="index">
            <div class="tile"
              :class="{ inProgress: tile.inGameProgress, scoredByUser: tile.scoredByUser, scoredByPc: tile.scoredByPc }"
              :ref="`tile${tile}`" @click="clickOnProgressItem(tile)">
            </div>
          </div>
        </div>
      </div>
    </div>
    <GameFooter  :userScore="userScore" :pcScore="pcScore" />

    <ResultModal v-if="resultsModal" :userScore="userScore" :pcScore="pcScore" @close="setDefaults" />
  </div>
</template>
<script>

import ResultModal from '@/components/ResultModal'
import GameFooter from '@/components/GameFooter'
import GameInput from '@/components/GameInput'

export default {
  name: 'MiniGame',
  components: {
    ResultModal, GameFooter, GameInput
  },
  data() {
    return {
      userScore: 0,
      pcScore: 0,
      timer: 1000,
      tiles: Array.from({ length: 100 }, () => ({ inGameProgress: false, scoredByUser: false, scoredByPc: false })),
      timeout: null,
      resultsModal: false,
      gameInProgress: false
    }
  },
  mounted() {
  },
  computed: {
    validArray() {
      return this.tiles.filter(item => !(item.inGameProgress === true || item.scoredByUser === true || item.scoredByPc === true))
    },

    hasWiner() {
      return this.userScore === 10 || this.pcScore === 10
    }
  },
  methods: {
    checkWiner() {
      if(this.hasWiner) {
        this.showResults()
        this.gameInProgress = false
        return
      }

      this.startTheGame()
    },
    setPointToPc(item) {
      item.scoredByPc = true
      item.inGameProgress = false
        this.pcScore++
        this.checkWiner()
    },

    setPointToUser(item) {
      item.scoredByUser = true
      item.inGameProgress = false
        this.userScore++
        this.checkWiner()
    },

    startTheGame() {
      this.gameInProgress = true
      const tileToChange = this.getRandomElement()
      tileToChange.inGameProgress = true
      this.timeout = setTimeout(() => {
        this.setPointToPc(tileToChange)
      }, this.timer)
    },
    getRandomElement() {
      return this.validArray[Math.floor(Math.random() *  this.validArray.length)]
    },
    clickOnProgressItem(item) {
      if (!item.inGameProgress) return
      clearTimeout(this.timeout)
      this.setPointToUser(item)
    },
    showResults() {
      this.resultsModal = true
    },
    setDefaults() {
      this.timer = 1000
      this.userScore = 0
      this.pcScore = 0
      this.tiles = Array.from({ length: 100 }, () => ({ inGameProgress: false, scoredByUser: false, scoredByPc: false }))
      this.timeout = null
      this.resultsModal = false
    }
  }
}
</script>
<style lang="scss" scoped>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800;900&display=swap');

.theGame {
  font-family: Inter, sans-serif;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 30px;
  background-color: #2E3044;
  text-transform: uppercase;
  font-weight: 700;

  .tilesWrapBg {
    height: 600px;
    width: 600px;
    display: flex;
    justify-content: center;
    align-items: center;
    border-radius: 25px;
    background: linear-gradient(134.94deg, #86E8BD 0.66%, #90B9FB 12.65%, #B3A4FE 26.48%, #DDA9EF 43.28%, rgba(239, 178, 230, 0.3) 65.01%, rgba(239, 178, 230, 0) 98.59%);
    box-shadow: 0px 24px 64px 0px #0000004D;

    .tilesWrap {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 596px;
      width: 596px;
      background: #0C0D11;
      position: relative;
      border-radius: 25px;

      .tiles {
        display: flex;
        flex-wrap: wrap;
        height: 500px;
        width: 500px;

        .tileItem {
          width: 50px;
          height: 50px;
          display: flex;
          justify-content: center;
          align-items: center;

          .tile {
            background-color: #246BFD;
            height: 90%;
            width: 90%;
            border-radius: 2px;
            transition: all .1s ease;
            cursor: pointer;

            &:hover {
              transform: scale(1.08);
            }
          }

          .inProgress {
            background-color: #FFD861;
          }

          .scoredByUser {
            background-color: #73FFA1;
          }

          .scoredByPc {
            background-color: #E02C2C;
          }
        }
      }
    }
  }
}
</style>