<template>
  <div class="home">
    <profile />
  </div>
</template>

<script>
// @ is an alias to /src
import Profile from "@/components/Profile.vue";

export default {
  name: "home",
  components: {
    Profile
  }
};
</script>

<style>
body {
  background-color: #444;
  margin: 0;
}
</style>

