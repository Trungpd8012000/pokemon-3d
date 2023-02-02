<template>
  <div class="list-card">
    <div
      class="list-card__inner"
      :style="{
        width: `${
          ((((625 - 94) / Math.sqrt(cardsContext.length) - 10) * 3) / 4 + 20) *
          Math.sqrt(cardsContext.length)
        }px`,
      }"
    >
      <card-game
        v-for="(card, index) in cardsContext"
        :key="index"
        :imgBackFaceUrl="`images/${card}.png`"
        :card="{ index, value: card }"
        @onFlip="handleFlip"
        :ref="`card-${index}`"
        :cardsContext="cardsContext"
      />
    </div>
    <copy-right />
  </div>
</template>

<script>
import Card from "./Card.vue";
import CopyRight from "./CopyRight.vue";
export default {
  data() {
    return {
      dataFlip: [],
    };
  },
  props: {
    cardsContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  components: {
    CopyRight,
    CardGame: Card,
  },
  methods: {
    handleFlip(card) {
      const elementFind = this.dataFlip.find(
        (item) => item.index === card.index
      );
      if (elementFind) {
        this.dataFlip = this.dataFlip.filter(
          (item) => item.index !== card.index
        );
      } else this.dataFlip = [...this.dataFlip, card];
      if (
        this.dataFlip.length === 2 &&
        this.dataFlip[0].value === this.dataFlip[1].value
      ) {
        this.$refs[`card-${this.dataFlip[0].index}`][0].onEnableDisabled();
        this.$refs[`card-${this.dataFlip[1].index}`][0].onEnableDisabled();

        const elementDisableds = document.querySelectorAll(
          ".list-card .card.disabled"
        );

        if (elementDisableds.length === this.cardsContext.length - 2) {
          setTimeout(() => {
            this.$emit("onFinish");
          }, 800);
        }
        this.dataFlip = [];
      } else if (
        this.dataFlip.length === 2 &&
        this.dataFlip[0].value !== this.dataFlip[1].value
      ) {
        setTimeout(() => {
          this.$refs[`card-${this.dataFlip[0].index}`][0].onFlipBackCard();
          this.$refs[`card-${this.dataFlip[1].index}`][0].onFlipBackCard();
          this.dataFlip = [];
        }, 800);
      } else return false;
    },
  },
};
</script>

<style lang="css" scoped>
.list-card {
  width: 100%;
  margin: auto;
  text-align: center;
  background: var(--bg-dark);
  color: var(--text-light);
  position: fixed;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
}
.list-card__inner {
  margin: 30px auto 0;
}
</style>
