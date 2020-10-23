<template>
  <div id="app">
    <!-- You can easily access everything that is in the data function -->
    <h1>{{user.username}}</h1>
    <h1>{{fullName}}</h1>
    <h1>Followers: {{followers}}</h1>
    <input @click="followPeople" type="button" value="Follow">
  </div>
</template>

<script>


export default {
  name: 'App',
  data(){
    return{
      followers: 0,
      user: {
        id: 1,
        username: '@thiomark',
        firstName: 'Thio',
        lastName: 'Mark',
        email: 'something@gmail.com',
        isAdmin: true
      }
    }
  },
  computed: {
    fullName(){
      return `${this.user.firstName} ${this.user.lastName}`
    }
  },
  methods: {
    followPeople(){
      this.followers ++
    }
  },
  // This will run when ever the page i refreshed
  // I think is like on onload when using vanilla javascript
  mounted() {
    this.followers ++
  },

  // This will watch and wait for something to change
  watch: {
    followers(newFollowersCount, oldFollowersCount){
      if(oldFollowersCount < newFollowersCount){
        console.log(`${this.user.username} has gained a follower`)
      }
    }
  }
 
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1{
  font-size: 14px;
}
</style>
