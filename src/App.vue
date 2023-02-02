<template>
  <main-screen v-if="statusGame === 'default'" @onReady="handleOnReady" />
  <interact-screen
    v-if="statusGame === 'match'"
    :cardsContext="settings.cardsContext"
    @onFinish="handleFinish"
  />
  <result-screen
    v-if="statusGame === 'result'"
    @onStartAgain="handleStartAgain"
    :timer="timer"
  />
</template>

<script>
import MainScreen from "./components/MainScreen.vue";
import InteractScreen from "./components/InteractScreen.vue";
import { sortRandom } from "./utils/array";
import ResultScreen from "./components/ResultScreen.vue";

export default {
  data() {
    return {
      settings: {
        amountOfCards: 0,
        cardsContext: [],
        startedAt: null,
      },
      statusGame: "default",
      timer: 0,
    };
  },
  components: {
    MainScreen,
    InteractScreen,
    ResultScreen,
  },
  methods: {
    handleOnReady(amount) {
      this.settings.amountOfCards = amount;
      this.statusGame = "match";
      const firstCards = Array.from(
        { length: amount / 2 },
        (_, index) => index + 1
      );
      const secondCards = [...firstCards];
      const cards = [...firstCards, ...secondCards];
      this.settings.cardsContext = sortRandom(cards);
      this.settings.startedAt = new Date().getTime();
    },
    handleFinish() {
      this.timer = new Date().getTime() - this.settings.startedAt;
      console.log(this.settings.startedAt);

      this.statusGame = "result";
    },
    handleStartAgain() {
      this.statusGame = "default";
    },
  },
};
</script>
