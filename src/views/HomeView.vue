<template>
  <div class="home">
    <submit-name />
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
