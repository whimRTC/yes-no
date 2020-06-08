<template>
  <div class="result-container">
    <h2>{{ $whim.state.question }}</h2>
    <p class="result"><span v-text="count" />人</p>
    <a class="fuwatto_btn_turquoise" @click="reset">次の質問へ</a>
  </div>
</template>
<script>
import questions from "@/questions";
import _ from "lodash";

export default {
  name: "result",
  computed: {
    appState() {
      return this.$whim.state;
    },
    users() {
      return this.$whim.users;
    },
    count: function() {
      return (
        this.users.length > 0 &&
        this.users.filter(user => this.appState[user.id] == "yes").length
      );
    }
  },
  methods: {
    reset() {
      if (Object.keys(this.$whim.state.indexes).length == questions.length) {
        this.$whim.assignState({ indexes: [] });
      }
      const candidates = _.difference(
        [...Array(questions.length).keys()],
        Object.keys(this.$whim.state.indexes).map(Number)
      );
      const index = candidates[Math.floor(Math.random() * candidates.length)];
      this.$whim.resetState({
        question: questions[index],
        indexes: this.$whim.state.indexes
      });
      this.$whim.assignState({
        indexes: { [index]: true }
      });
    }
  }
};
</script>
<style>
.result-container {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: white;
  border: solid;
  padding: 20px;
  text-align: center; /*一応BOX内の文字も中央寄せ*/
}
.result {
  font-size: 50px;
  font-weight: bold;
  color: red;
}
.fuwatto_btn_turquoise {
  display: block;
  background-color: turquoise;
  color: #fff;
  padding: 0.8em;
  text-decoration: none;
  border-radius: 4px;
  box-shadow: 0 2px 2px 0 rgba(0, 0, 0, 0.12), 0 1px 5px 0 rgba(0, 0, 0, 0.12),
    0 3px 1px -2px rgba(0, 0, 0, 0.2);
  transition: 0.3s ease-out;
  width: 200px;
  margin: 0px auto;
}
.fuwatto_btn_turquoise:hover {
  cursor: pointer;
  text-decoration: none;
  box-shadow: 0 5px 10px 0 rgba(0, 0, 0, 0.12), 0 3px 20px 0 rgba(0, 0, 0, 0.12),
    0 5px 6px -2px rgba(0, 0, 0, 0.2);
}
</style>
