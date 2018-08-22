<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <tweets />
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";
import Tweets from "@/components/Tweets.vue";

export default {
  name: "home",
  components: {
    HelloWorld,
    Tweets
  }
};
</script>

<style>
body {
  background-color: #444;
  margin: 0;
}
</style>

