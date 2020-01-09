<template>
  <div>
    <!-- <div v-if="error" style="color: red">{{error}}</div>
    <div v-else style="">
      <div>
        <h1 style="margin:0; color:purple">{{response.data.name}}</h1>
        <h2 style="margin:0; font-size:16px; color: white;">{{response.data.race.name}} {{response.data.character_class.name}}</h2>
        <img src="https://render-us.worldofwarcraft.com/character/moon-guard/89/141749593-avatar.jpg" style="width:250px; margin-top:30px;" />
        
      </div>
    </div> -->
  
    <div v-if="response">
      <!-- <p>{{response.data.name}}</p> -->
    </div>
    <div>
      <input  type="text" v-model="userInputServer">
      <input type="text" v-model="userInputName">
      <button @click="getCharacter(userInputServer, userInputName), getThumbnail(userInputServer, userInputName)">Search</button>
      <button @click="getChar()">debug</button>
    </div>
    <div>
      <div v-for="character in characters" v-bind:key="character.id">
        <p>{{character.name}}</p>
        <p>{{character.realm.name}}</p>
        <img src="http://render-{region}.worldofwarcraft.com/character/{character.thumbnail}">
      </div>
      
    </div>
  </div>
</template>

<script>
import axios from "axios";
//import { response } from 'express';

export default {
  
  // mounted: async function() {
  //   try {
  //     let response = await axios.get(
  //       "https://us.api.blizzard.com/profile/wow/character/" + userInput + "/kanaestia?namespace=profile-us&locale=en_US&access_token=US161L3oBgWKNJmx7qSvdxM6NB7n58SlnA"
  //     );
  //     this.response = response;
  //   } catch (error) {
  //     this.error = error;
  //   }
  // },
  data() {
    return {
      log: "no text",
      response: {},
      error: "",
      userInputServer: "",
      userInputName: "",
      characters: [],
      thumbnails: []
    };
  },
  methods: {
    async getCharacter(server, name) {
      try {
      let response = await axios.get(
        "https://us.api.blizzard.com/profile/wow/character/" + server + "/" + name + "?namespace=profile-us&locale=en_US&access_token=US2B2jTNzSC4j3lVY5G91ha9Np667792nL",
        );

      /* if (typeof.server == String) {
      } */
      this.response = response;
      this.characters.push(this.response.data)
      
    } catch (error) {
      this.error = error;
    }
    },
    
     async getThumbnail(userInputServer, userInputName) {
      try {
      let response = await axios.get(
        "https://us.api.blizzard.com/profile/wow/character/" + userInputServer + "/" + userInputName + "/character-media?namespace=profile-us&locale=en_US&access_token=USm5eeka21GQfFtZb4cvXaxYhJ4389yXll"
        );
     

      //  if (typeof.server == String) {
      // } 
      this.response = response;
      this.thumbnails.push(this.response.data)
      console.log(this.thumbnails)
      
    } catch (error) {
      this.error = error;
    }
    },
    
    getChar: function() {
      /* eslint-disable no-console */ 
      /*console.log(this.response.data);*/
      console.log(this.response.data)
    }
    },
};
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

