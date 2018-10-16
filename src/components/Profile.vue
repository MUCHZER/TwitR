<template>
  <v-layout align-center>
    Welcome {{ user_details.screen_name }}

    <uploader />

    <v-btn depressed small :to="'eraser'">Let's go!</v-btn>

  </v-layout>
</template>

<script>
import Uploader from "@/components/Uploader.vue";

export default {
  name: "Profile",
  components: {
    Uploader
  },
  data() {
    return {
      user_details: {}
    };
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
