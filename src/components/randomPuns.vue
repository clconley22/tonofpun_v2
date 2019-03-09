<template>
  <div class="hello">
     <h1>{{ status }}</h1>
     <h2>{{ punchline }}</h2>

  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'randomPuns',
  data () {
    return {
      status: '',
      punchline: ''
    }
  },
  created () {
    this.loadQuote();
  },
  methods: {
    loadQuote() {
      this.status = 'Loading...';
      var vm = this;
      axios.get('https://official-joke-api.appspot.com/jokes/random')
      .then(response => {
        vm.status = response.data.setup;
        vm.punchline = response.data.punchline;
      })
      .catch(error => {
        vm.status = 'An error occurred.' + error;
        vm.punchline = 'An error occurred.' + error;
      });
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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
