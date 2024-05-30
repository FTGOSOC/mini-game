<template>
    <div class="gameHeader">
        <div class="timer">
            <input type="number" v-model="timer" :disabled="gameInProgress">
        </div>
        <div class="startButton">
            <button class="startButton" @click="$emit('start')" :disabled="gameInProgress">
                Почати
            </button>
        </div>
    </div>
</template>

<script>
    export default {
        name: "GameInput",

        props: {
            value: {
                type: Number,
                requred: true,
            },

            gameInProgress: {
                type: Boolean,
                default: false,
            }
        },

        computed: {
            timer: {
                get() {
                    return this.value
                },
                set(val) {
                    this.$emit("input", +val)
                }
            }
        }
    }
</script>

<style lang="scss" scoped>
  .gameHeader {
    display: flex;
    justify-content: space-between;
    width: calc(600px - 17px * 2);
    background: #0C0D11;
    border-radius: 20px;
    padding: 15px 17px;
    box-shadow: 0px 24px 64px 0px #0000004D;

    .timer {
      input {
        background: #191919;
        color: #fff;
        outline: none;
        border: none;
        padding: 0 14px;
        border-radius: 10px;
        height: 40px;
        font-family: Inter, sans-serif;
        font-size: 18px;
        font-weight: 400;
        line-height: 25.6px;
        text-align: left;
        -webkit-appearance: textfield;
        -moz-appearance: textfield;
        appearance: textfield;
        &::-webkit-inner-spin-button {
          -webkit-appearance: none;
          margin: 0;
        }
        &:disabled {
          background-color: #ccc;
        }
      }
    }

    .startButton {
      button {
        cursor: pointer;
        background-color: #246BFD;
        outline: none;
        border: none;
        padding: 0 24px;
        font-family: Inter, sans-serif;
        font-size: 18px;
        font-weight: 800;
        line-height: 21.78px;
        color: #fff;
        height: 40px;
        border-radius: 10px;
        &:disabled {
          background-color: #ccc;
        }
      }
    }
  }
</style>