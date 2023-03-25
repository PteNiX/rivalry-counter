
<script lang="ts">


export default{
  data() {
    return {
     player1:{
      tag:"",
     },
     player2:{
      tag:"",
     },
     tagReturn:[],
     tagReturn2:[],
     urlTag:``,
     urlTag2:``,
     urlGames1:'',
     urlGames2:'',
     
  }

},   
methods: {

  async urlFunctionPlayer1() {

    if (this.player1.tag.length > 2) {
    this.urlTag= `https://website-backend.w3champions.com/api/players/global-search?search=${this.player1.tag}&pageSize=20`;
const resTag  = await fetch(this.urlTag);
const dataTag  = await resTag.json();
this.tagReturn =  dataTag;
    }
},

async urlFunctionPlayer2() {

  if (this.player2.tag.length > 2) {
this.urlTag2= `https://website-backend.w3champions.com/api/players/global-search?search=${this.player2.tag}&pageSize=20`;
const resTag2  = await fetch(this.urlTag2);
const dataTag2  = await resTag2.json();
this.tagReturn2 =  dataTag2;

  }

  
},

async showRivalry () {
   


  for(let i=2; i<15; i++) {
this.urlGames1 = `https://website-backend.w3champions.com/api/matches/search?playerId=${this.player1.tag.trim().replace('#', '%23')}&gateway=0&offset=0&pageSize=100&season=${i}&gamemode=1`
 
this.urlGames1 =`https://website-backend.w3champions.com/api/matches/search?playerId=${this.player1.tag.trim().replace('#', '%23')}&gateway=20&offset=0&opponentId=${this.player2.tag.trim().replace('#', '%23')}&pageSize=50&season=${i}&gamemode=1`;

  console.log (this.urlGames1);


}
}
}
}



</script>


<template>
  

    <input class="input-player1" type='text' v-model="player1.tag" list="player1" v-on:input="urlFunctionPlayer1()">
    <datalist id="player1" class="tag" >
    <option v-for="tag in tagReturn"> {{tag.battleTag}} </option>
   </datalist>

    <input class="input-player2" type='text' v-model="player2.tag" list="player2" v-on:input="urlFunctionPlayer2()">
    <datalist id="player2" class="tag2" >
    <option v-for="tag2 in tagReturn2"> {{tag2.battleTag}} </option>
   </datalist>
   
   <br>

   <button class="button-show" v-on:click="showRivalry"> Show</button>

</template>

<style scoped>

</style>
