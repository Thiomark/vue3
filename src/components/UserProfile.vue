<template>
  <div class="user-profile">
    <div class="user-profile_user-panel">
        <h1 class="user-profile_username">@{{user.username}}</h1>
        <h1 class="the-admim" v-if="user.isAdmin">Admin</h1>
        <h1 class="the-admim" v-else>Not Admin</h1>
        <div class="user-profile_follower-count">
            <strong>Followers: {{followers}}</strong>
        </div> 
    </div>
    <div class="posted-twoots">
      <UserMessage v-for="twoot in user.twoots" :key="twoot.id" :username="user.username" :twoot="twoot" @favourite="toggleFavourite"/>
    </div>
  </div>
</template>

<script>

import UserMessage from './MessageItems.vue'

export default {
  name: 'UserProfile',
  components: {
    UserMessage
  },
  data(){
    return{
      followers: 0,
      user: {
        id: 1,
        username: 'thiomark',
        firstName: 'Thio',
        lastName: 'Mark',
        email: 'something@gmail.com',
        isAdmin: false,
        twoots: [
          {id: 1, message: "My first twoot guys"},
          {id: 2, message: "I hate earch guys"}
        ]
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
    },
    toggleFavourite(id){
      console.log(`Favor twoot ${id}`)
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
.user-profile{
    display: grid;
    grid-template-columns: 1fr 3fr;
    width: 100%;
    padding: 50px 5%;
    
}

.user-profile_user-panel{
    display: flex;
    flex-direction: column;
    margin-right: 50px;
    padding: 20px;
    background-color: rgb(248, 248, 248);
    border-radius: 5px;
    border: 1px solid #DFE3E8;
    font-size: 14px;
}

.the-admim{
  background-color: rgb(153, 39, 153);
  color: #ffffff;
  border-radius: 5px;
  margin: auto;
  padding: 10px 10px;
  font-weight: bold;
  font-size: 13px;
}

.just-line{
  color: black;
}

h1 {
    margin: 0;
}

</style>