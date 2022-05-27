<template>
  <div class="home">
    <!-- <img alt="Vue logo" src="../assets/logo.png"> -->
    <submit-name msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
// @ is an alias to /src
import SubmitName from '@/components/SubmitName.vue'

export default {
  name: 'HomeView',
  components: {
    SubmitName
  }
}
</script>
