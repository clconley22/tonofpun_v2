<template>
  <div class="hello">
     <h1>{{ pun }}</h1>
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
      axios.get('https://getpuns.herokuapp.com/api/random')
      .then(response => {
        vm.pun = response.data
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


</style>


<!--
Notes
* connect pun api or find new pun api
* style
* animate
* push live to tonofpun.com

-->
