<template>
  <div id="app">
    <Player
      v-for="user in $whim.users"
      :key="user.id"
      :class="whimUserWindowClass(user)"
      :displayUser="user"
    />

    <Main class="main" />
  </div>
</template>

<script>
export default {
  name: "App",
  components: {
    Main: () => import("@/components/main/Index"),
    Player: () => import("@/components/player/Index")
  }
};
</script>

<style lang="scss" scoped></style>
