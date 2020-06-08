<template>
  <div class="selecting-container">
    <h2>{{ $whim.state.question }}</h2>
    <div v-if="isSelected" class="answer">
      <h2>選択済み</h2>
    </div>
    <div v-else class="answer">
      <p class="answer-yes" @click="answer('yes')">Yes</p>
      <p class="answer-no" @click="answer('no')">No</p>
    </div>
  </div>
</template>
<script>
export default {
  name: "Selecting",
  computed: {
    isSelected() {
      return !!this.$whim.state[this.$whim.accessUser.id];
    }
  },
  methods: {
    answer(bool) {
      this.$whim.assignState({
        [this.$whim.accessUser.id]: bool
      });
    }
  }
};
</script>

<style lang="scss" scoped>
.selecting-container {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: white;
  border: solid;
  padding: 20px;
  text-align: center;
}
.answer {
  display: flex;
  justify-content: center;
  cursor: pointer;
  .answer-yes {
    color: white;
    background-color: blue;
    border-radius: 4px;
    padding: 15px 40px;
    margin-right: 20px;
  }

  .answer-no {
    color: white;
    background-color: red;
    border-radius: 4px;
    padding: 15px 40px;
  }
}
</style>
