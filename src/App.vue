<template>
  <div id="app">
    <UserProfile />
  </div>
</template>

<script>
import UserProfile from './components/UserProfile.vue'
export default {
  name: 'App',
  components: {
    UserProfile
  }
}
</script>

<style>
#app {
  font-family: 'Roboto', sans-serif;
  width: 100vw;
}
</style>