<template>
  <div class="user-profile">
    <div class="user-profile_user-panel">
        <h1 class="user-profile_username">@{{user.username}}</h1>
        <h1 class="the-admim" v-if="user.isAdmin">Admin</h1>
        <h1 class="the-admim" v-else>Not Admin</h1>
        <div class="user-profile_follower-count">
            <strong>Followers: {{followers}}</strong>
        </div> 
        <form class="twoot-panel" @submit.prevent="createNewTwoot" >
          <label>New twoot {{numOfCharUsed}}/180</label>
          <textarea cols="30" rows="10" v-model="newTwootContent" :class="{'overTheLimit': numOfCharUsed > 180}"></textarea>
          <div class="typeOfTwoot">
          <label for="newTwootType">Type: </label>
          <select id="newTwootType" v-model="selectedTwootType">
            <option :value="option.value" v-for="(option, index) in twootType" :key="index"> {{ option.name }} </option>
          </select>
          <br>
          <button id="theSubmitButton" :class="{'hideTheSubmitButton': numOfCharUsed > 180}">
            Twoot
          </button>
        </div>
        </form>
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
      selectedTwootType: 'instant',
      newTwootContent: "",
      twootType: [
        {value: 'draft', name: 'Draft'},
        {value: 'instant', name: 'Instant Twoot'}
      ],
      followers: 0,
      user: {
        id: 1,
        username: 'thiomark',
        firstName: 'Thio',
        lastName: 'Mark',
        email: 'something@gmail.com',
        isAdmin: false,
        twoots: [
          {id: 1, message: "My first message"},
          {id: 2, message: "my second message"}
        ]
      }
    }
  },
  computed: {
    numOfCharUsed(){
      return this.newTwootContent.length
    },

    fullName(){
      return `${this.user.firstName} ${this.user.lastName}`
    }
  },
  methods: {
    createNewTwoot(){
      console.log('1')
      if(this.newTwootContent && this.selectedTwootType === "instant"){
        console.log('2')
        this.user.twoots.unshift({
          id: this.user.twoots.length + 1,
          message: this.newTwootContent
        })
        this.newTwootContent = ""
      }
    },
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

<style >
.user-profile_username{
  font-size: 15px;
  font-weight: bolder;
}

.create-the-twot{
  padding-top: 20px;
  display: flex;
  flex-direction: column;
}

.overTheLimit{
  border: 1px soild red;
  background-color: red;
}

.hideTheSubmitButton{
  visibility: hidden;
}

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
  text-align: center;
  background-color: rgb(153, 39, 153);
  color: #ffffff;
  border-radius: 5px;
  padding: 2px 2px ;
  font-weight: bold;
  font-size: 13px;
  width: 70px;
}

.twoot-panel {
  margin-top:  5px;
}

.just-line{
  color: black;
}

h1 {
    margin: 0;
}

</style>