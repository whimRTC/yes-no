<template>
  <div>
    <Selecting v-show="isSelecting" />
    <Result v-show="isAllSelected" />
  </div>
</template>

<script>
import questions from "@/questions";

export default {
  name: "Main",
  components: {
    Selecting: () => import("@/components/main/Selecting"),
    Result: () => import("@/components/main/Result")
  },
  computed: {
    appState() {
      return this.$whim.state;
    },
    users() {
      return this.$whim.users;
    },
    isAllSelected() {
      return (
        this.users.length > 0 &&
        this.users.every(user => this.appState[user.id])
      );
    },
    isSelecting() {
      return !this.isAllSelected;
    }
  },
  mounted() {
    if (!this.$whim.state.question) {
      const index = Math.floor(Math.random() * questions.length);
      this.$whim.assignState({
        question: questions[index],
        indexes: { [index]: true }
      });
    }
  }
};
</script>

<style></style>
