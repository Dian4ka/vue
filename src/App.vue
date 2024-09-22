<template>
  <UserCard />
</template>

<script>
import UserCard from "./components/user-card.vue";

export default {
  name: "App",
  components: {
    UserCard,
  },
};
</script>

<style>
html, body {
  margin: 0;
  font-family: Verdana, Geneva, Tahoma, sans-serif;
}
</style>