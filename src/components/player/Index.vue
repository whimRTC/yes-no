<template>
  <div class="container">
    <div v-if="!isAllSelected & isSelected" class="label">
      <div class="text">選択済み</div>
    </div>
    <div v-else-if="!isAllSelected" class="label">
      <div class="text">選択中</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Player",
  props: ["displayUser"], // 表示されているUserの情報
  computed: {
    appState() {
      return this.$whim.state || {};
    },
    userId() {
      return this.$whim.accessUser.id;
    },
    displayUserId() {
      return this.displayUser.id;
    },
    users() {
      return this.$whim.users;
    },
    isMe() {
      return this.userId === this.displayUserId;
    },
    isSelected() {
      return !!this.appState[this.displayUserId];
    },
    isAllSelected() {
      return (
        this.users.length > 0 &&
        this.users.every(user => this.appState[user.id])
      );
    }
  }
};
</script>

<style lang="scss" scoped>
.container {
  text-align: center;
}
.label {
  display: inline-block;
  position: relative;
  margin: 0 auto;
  top: 30%;
  background: #ffffff50;
  border-radius: 5px;
  padding: 1px 5px;
}
.text {
  font-size: 30px;
  font-weight: bold;
}
</style>
