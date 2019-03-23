<template>
  <div class="hello">
    <div class="punContainer">
      <h1>{{ pun }}</h1>
    </div>
     <!-- <sui-button @click="show = !show">Show me the answer</sui-button> -->
     <!-- <h2 v-if="show"> {{ punchline }} </h2> -->
     <div>
      <sui-button animated id="change" @click="newPun">
        <sui-button-content visible>Next Pun</sui-button-content>
          <sui-button-content hidden>
          <sui-icon name="right arrow" />
        </sui-button-content>
      </sui-button>
     </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'randomPuns',
  data () {
    return {
      pun: '',
      show: false,
      myColor: '888888'
    }
  },
  created () {
    this.loadJoke();
  },
  methods: {
    loadJoke() {
      this.pun = 'Loading...';
      var vm = this;
      axios.get('https://cors-anywhere.herokuapp.com/https://getpuns.herokuapp.com/api/random')
      .then(response => {
        vm.pun = response.data.Pun;
      })
      .catch(error => {
        vm.pun = 'An error occurred. ' + error;
      });
    },
    generator() {
        this.mycolor = '#'+(Math.random()*0xFFFFFF<<0).toString(16)
        document.body.style.background = this.mycolor
      },
    newPun() {
      this.loadJoke()
      this.generator()
      return this.show = false;
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.punContainer {
  margin: 0 auto;
  width: 60%;
}

.ui.animated.button{
  margin-top:20px;
}

@media screen and (max-width: 600px) {
  .punContainer {
    width: 90%;
  }
}
</style>


<!--
Notes
* connect pun api or find new pun api
* style
* animate
* push live to tonofpun.com

-->
