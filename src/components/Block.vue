// * Create status to wait for random delay [x]
// * Use setTimeout function with the delay prop to show block [x]
// * Start timer as block appears []
  // ! Create functions (start/stop) and correspondent variables

<template>
  <div class="block" v-if="showBlock" @click="stopTimer">Click Me!</div>
</template>

<script>
export default {
  props: ["delay"],
  data() {
    return {
      showBlock: false,
      timer: null,
      reactionTime: 0,
    };
  },
  mounted() {
    // console.log("component mount");
    setTimeout(() => {
      this.showBlock = true;
      this.startTimer();
    }, this.delay);
  },
  methods: {
    startTimer() {
      this.timer = setInterval(() => {
        this.reactionTime += 10;
      }, 10);
    },
    stopTimer() {
      clearInterval(this.timer);
      // console.log(this.reactionTime);
      this.$emit("end", this.reactionTime);
    },
  },
  //   updated() {
  //     console.log("component updated");
  //   },
  //   unmounted() {
  //       console.log('unmounted')
  //   }
};
</script>

<style>
.block {
  width: 400px;
  border-radius: 20px;
  background: #42b883;
  color: white;
  text-align: center;
  padding: 100px 0;
  margin: 40px auto;
}

/* Vue colors: #42b883 | #35495e */
</style>