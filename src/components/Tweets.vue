<template>
  <div class="">
    <vue-swing
      @throwout="onThrowout"
      :config="config"
      ref="vueswing"
    >
      <div
        v-for="tweet in tweets"
        :key="tweet.id"
        class="tweet"
      >
        <span>{{ tweet.content }}</span>
      </div>
    </vue-swing>
  </div>
</template>

<script>
import VueSwing from "vue-swing";

export default {
  name: "Tweets",
  components: { VueSwing },
  props: {
    content: String
  },
  data() {
    return {
      config: {
        allowedDirections: [VueSwing.Direction.LEFT, VueSwing.Direction.RIGHT],
        minThrowOutDistance: 250,
        maxThrowOutDistance: 300
      },
      tweets: [
        {
          id: 1,
          content: "test1"
        },
        {
          id: 2,
          content: "test2"
        },
        {
          id: 3,
          content: "test3"
        },
        {
          id: 4,
          content: "test4"
        }
      ]
    };
  },
  methods: {
    remove() {
      this.swing();
      setTimeout(() => {
        this.cards.pop();
      }, 100);
    },
    swing() {
      const cards = this.$refs.vueswing.cards;
      cards[cards.length - 1].throwOut(
        Math.random() * 100 - 50,
        Math.random() * 100 - 50
      );
    },
    onThrowout({ target, throwDirection }) {
      console.log(`Threw out ${target.textContent}!`);
    }
  }
};
</script>

<style lang="scss" scoped>
.tweet {
  color: black;
  align-items: center;
  background-color: #fff;
  border-radius: 20px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  display: flex;
  font-size: 72px;
  height: 200px;
  justify-content: center;
  left: calc(50% - 100px);
  position: absolute;
  top: calc(50% - 100px);
  width: 200px;
}
</style>


