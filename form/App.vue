<template>
  <div class="form">
    <signUp />
  </div>
</template>

<script>
import signUp from '@/components/signUp/signUp.vue';

export default {
  name: 'App',
  components: {
    signUp
  }
}
</script>

<style lang="scss">
@import './main'
</style>
