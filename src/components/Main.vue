
<script lang="ts">


export default{
  data() {
    return {
     player1:{
      tag:"",
     },
     tagReturn:[],
     urlTag:``,
     url:[]
     
  }

},   
methods: {

  async urlFunction() {

    this.urlTag= `https://website-backend.w3champions.com/api/players/global-search?search=${this.player1.tag}&pageSize=20`;
const resTag  = await fetch(this.urlTag);
const dataTag  = await resTag.json();

this.tagReturn =  dataTag;






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
<button class="button" v-on:click="urlFunction" > Count</button>

  </div>
</template>

<style scoped>

</style>
