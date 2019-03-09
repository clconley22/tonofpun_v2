<template>
  <div class="home">
    <randomPuns/>
  </div>
</template>

<script>
// @ is an alias to /src
import randomPuns from '@/components/randomPuns.vue'

export default {
  name: 'home',
  components: {
    randomPuns
  }
}
</script>
