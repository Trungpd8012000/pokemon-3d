<template>
  <div
    class="card"
    :class="{ disabled: isDisabled }"
    :style="{
      height: `${(625 - 94) / Math.sqrt(cardsContext.length) - 10}px`,
      width: `${
        (((625 - 94) / Math.sqrt(cardsContext.length) - 10) * 3) / 4
      }px`,
      perspective: `${
        (((625 - 94) / Math.sqrt(cardsContext.length) - 10) * 3) / 4
      }px`,
    }"
  >
    <div
      class="card__inner"
      :class="{ 'is-flipped': isFlipped }"
      @click="onFlipped"
    >
      <div class="card__face card__face--front">
        <div
          class="card__content"
          :style="{
            backgroundSize: `${
              (((625 - 94) / Math.sqrt(cardsContext.length) - 10) * 3) / 4 / 2
            }px ${
              (((625 - 94) / Math.sqrt(cardsContext.length) - 10) * 3) / 4 / 2
            }px`,
          }"
        ></div>
      </div>
      <div class="card__face card__face--back">
        <div
          class="card__content"
          :style="{
            background: `url(${require('@/assets/' +
              imgBackFaceUrl)}) no-repeat center center / contain`,
            backgroundSize: `${
              (((625 - 94) / Math.sqrt(cardsContext.length) - 10) * 3) / 4 / 1.5
            }px ${
              (((625 - 94) / Math.sqrt(cardsContext.length) - 10) * 3) / 4 / 1.5
            }px`,
            width: '100%',
            height: '100%',
          }"
        ></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isFlipped: false,
      isDisabled: false,
    };
  },
  props: {
    card: {
      type: [String, Number, Object],
    },
    imgBackFaceUrl: {
      type: String,
      require: true,
    },
    cardsContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  methods: {
    onFlipped() {
      if (this.isDisabled) return false;
      this.isFlipped = !this.isFlipped;
      if (this.isFlipped) this.$emit("onFlip", this.card);
    },
    onFlipBackCard() {
      this.isFlipped = false;
    },
    onEnableDisabled() {
      this.isDisabled = true;
    },
  },
};
</script>

<style scoped lang="css">
img {
  width: 100%;
  height: 100%;
}
.card {
  display: inline-block;
  margin: 0 10px 10px;
  border-radius: 10px;
  overflow: hidden;
}
.card.disabled .card__inner {
  cursor: default;
}
.card__inner {
  width: 100%;
  height: 100%;
  transform-style: preserve-3d;
  transition: 1s;
  cursor: pointer;
  position: relative;
}
.card__inner.is-flipped {
  transform: rotateY(-180deg);
}
.card__face {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;

  display: flex;
  justify-content: center;
  align-items: center;

  background: #000;
}
.card__face--front .card__content {
  background: url("../assets/images/icon_back.png") no-repeat center center;
  width: 100%;
  height: 100%;
}
.card__face--back {
  transform: rotateY(-180deg);
  background: rgb(27, 27, 26);
}
</style>
