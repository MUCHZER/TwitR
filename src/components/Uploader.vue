<template>
  <v-layout align-center>
    <v-btn depressed small @click="readZip">Read zip</v-btn>

    <div v-if="isLoading">
      Loading...
    </div>
    <div v-if="!isLoading && user_details && allTweets">
      Welcome {{ user_details.screen_name }}      
    </div>
  </v-layout>
</template>

<script>
import JSZip from "jszip";
import axios from "axios";
import Papa from "papaparse";

export default {
  name: "uploader",
  data() {
    return {
      isLoading: false,
      user_details: null,
      allTweets: null
    };
  },
  methods: {
    readZip() {
      this.isLoading = true;
      axios
        .get("/zip/126077553_b34952fca0df6a45384c87dbe7a23aa16c9e8994.zip", {
          responseType: "arraybuffer",
          headers: {
            "Content-Type": "application/zip",
            Accept: "application/zip, application/octet-stream"
          }
        })
        .then(response => {
          JSZip.loadAsync(response.data).then(zip => {
            Promise.all([
              // First we get user_details
              zip
                .file("data/js/user_details.js")
                .async("string")
                .then(data => {
                  // Removing JS markup so we get a JSON-like file and we can parse it
                  const json = data.replace("var user_details =  ", "");
                  this.user_details = JSON.parse(json);
                }),
              // Next we get our user tweets
              zip
                .file("tweets.csv")
                .async("string")
                .then(data => {
                  // Removing JS markup so we get a JSON-like file and we can parse it
                  Papa.parse(data, {
                    header: true,
                    complete: csv => {
                      this.allTweets = csv.data;
                      console.log(csv);
                      this.allTweets.forEach(e => {
                        console.log(e.tweet_id);
                      });
                    }
                  });
                })
            ]).then(() => {
              // Our work is finaly done
              this.isLoading = false;
            });
          });
        })
        .catch(error => console.log(error));
    }
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
