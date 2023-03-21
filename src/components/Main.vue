
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
     
     
  }

},   
methods: {

  async urlFunction() {

    this.urlTag= `https://website-backend.w3champions.com/api/players/global-search?search=${this.player1.tag}&pageSize=20`;
const resTag  = await fetch(this.urlTag);
const dataTag  = await resTag.json();
this.tagReturn =  dataTag;

this.urlTag2= `https://website-backend.w3champions.com/api/players/global-search?search=${this.player2.tag}&pageSize=20`;
const resTag2  = await fetch(this.urlTag);
const dataTag2  = await resTag2.json();
this.tagReturn2 =  dataTag2;




console.log (dataTag)

},


}

}

</script>


<template>
  <div class="greetings">
  
  {{ player1.tag }}
    <input class="input-player1" type='text' v-model="player1.tag" list="player1">
    <datalist id="player1" class="tag" >
    <option v-for="tag in tagReturn"> {{tag.battleTag}} </option>
   </datalist>
   {{ player2.tag }}
    <input class="input-player1" type='text' v-model="player1.tag" list="player2">
    <datalist id="player2" class="tag" >
    <option v-for="tag in tagReturn2"> {{tag.battleTag}} </option>
   </datalist>
<button class="button" v-on:click="urlFunction" > Count</button>

  </div>
</template>

<style scoped>

</style>
