<template>
  <div class="screen">
    <h2>Congratulation !</h2>
    <div class="time">
      <span>{{ Math.round(timer / 1000) }}</span> seconds
    </div>
    <button @click="onStartAgain">Start Again</button>
  </div>
</template>

<script>
export default {
  props: {
    timer: {
      type: Number,
      required: true,
    },
  },
  methods: {
    onStartAgain() {
      this.$emit("onStartAgain");
    },
  },
};
</script>

<style lang="css" scoped>
h2 {
  font-size: 30px;
  font-weight: bold;
}

.screen {
  width: 100%;
  height: 100vh;

  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;

  background: var(--bg-dark);
  color: var(--text-light);
}

.screen .time {
  margin: 14px 0;
}

.screen .time span {
  color: red;
  font-weight: bold;
}

.screen button {
  color: var(--text-light);
  background: var(--bg-dark);

  padding: 10px;
  border: 1px solid #000;

  transition: 0.3s;
}

.screen button:hover {
  cursor: pointer;

  background: #000;
}
</style>
