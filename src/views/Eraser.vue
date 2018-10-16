<template>
  <div class="home">
    <tweet-swig />
  </div>
</template>

<script>
// @ is an alias to /src
import TweetSwig from "@/components/TweetSwig.vue";

export default {
  name: "eraser",
  components: {
    TweetSwig
  }
};
</script>

<style>
body {
  background-color: #444;
  margin: 0;
}
</style>

