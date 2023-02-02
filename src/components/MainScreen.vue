<template>
  <div class="screen">
    <h1>POKEMON MEMORIES</h1>
    <h3>Select mode to start game</h3>
    <div class="modes">
      <div class="mode-item" @click="onReady(16)">
        <span>4x4</span>
        <span>Easy</span>
      </div>
      <div class="mode-item" @click="onReady(36)">
        <span>6x6</span>
        <span>Normal</span>
      </div>
      <div class="mode-item" @click="onReady(64)">
        <span>8x8</span>
        <span>Hard</span>
      </div>
      <div class="mode-item" @click="onReady(100)">
        <span>10x10</span>
        <span>Super Hard</span>
      </div>
    </div>
    <copy-right />
  </div>
</template>

<script>
import CopyRight from "./CopyRight.vue";

export default {
  components: {
    CopyRight,
  },
  methods: {
    onReady(amount) {
      this.$emit("onReady", amount);
    },
  },
};
</script>

<style lang="css" scoped>
.screen {
  width: 100%;
  height: 100vh;

  display: flex;
  justify-content: center;
  flex-direction: column;

  background: var(--bg-dark);
  color: var(--text-light);
}

h1,
h3 {
  text-align: center;
}

.screen .modes {
  display: flex;
  justify-content: center;

  margin: 1rem 0;
}

.screen .modes .mode-item {
  cursor: pointer;

  width: 100px;
  height: 100px;
  margin: 0 10px;
  border: 2px solid #fff;
  border-radius: 10px;

  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  transition: 0.3s;
}

.screen .modes .mode-item:hover {
  background: #000;
}
</style>
