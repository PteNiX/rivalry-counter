
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
     score1:0,
     score2:0,
     
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
/* this.urlGames1 = `https://website-backend.w3champions.com/api/matches/search?playerId=${this.player1.tag.trim().replace('#', '%23')}&gateway=0&offset=0&pageSize=100&season=${i}&gamemode=1` */
 
this.urlGames1 =`https://website-backend.w3champions.com/api/matches/search?playerId=${this.player1.tag.trim().replace('#', '%23')}&gateway=20&offset=0&opponentId=${this.player2.tag.trim().replace('#', '%23')}&pageSize=50&season=${i}&gamemode=1`;

const resScore  = await fetch(this.urlGames1);
const dataScore  = await resScore.json();

  console.log (dataScore);
  for (let i = 0; i < dataScore.matches.length; i++) {
    if (
      dataScore.matches[i].teams[0].players[0].battleTag == `${this.player1.tag.trim()}` &&
      dataScore.matches[i].teams[0].won == true
    ) {
      this.score1++;
    }
      else if (
      dataScore.matches[i].teams[0].players[0].battleTag == `${this.player1.tag.trim()}` &&
      dataScore.matches[i].teams[0].won == false
      ){
        this.score2++;
      }
  
    if (
      dataScore.matches[i].teams[1].players[0].battleTag == `${this.player1.tag.trim()}`  &&
      dataScore.matches[i].teams[1].won == true
      /* dataScore.matches[i].teams[1].players[0].race == `${this.mmrForm.race}` */
    ) {
      this.score1++;
    }
    else if (dataScore.matches[i].teams[1].players[0].battleTag == `${this.player1.tag.trim()}` &&
      dataScore.matches[i].teams[1].won == false){
        this.score2++;
      }
  }

  console.log(this.score1, this.score2);


}

let score1:any = document.querySelector('.score-player1');
let score2:any = document.querySelector('.score-player2');
  score1.innerHTML = this.score1;
  score2.innerHTML = this.score2;
  let namePlayer1:any = document.querySelector('.name-player1');
  let namePlayer2:any = document.querySelector('.name-player2');

  namePlayer1.innerHTML = this.player1.tag.trim().split('#')[0];
  namePlayer2.innerHTML = this.player2.tag.trim().split('#')[0];

this.score1=0;
this.score2=0;
}
}
}



</script>


<template>
  
  <div class="container">
    <div class="title"> W3Champions Rivalry Counter </div>
    <div class="form">

    <input class="input-player1 input" type='text' v-model="player1.tag" list="player1" v-on:input="urlFunctionPlayer1()">
    <datalist id="player1" class="tag" >
    <option v-for="tag in tagReturn"> {{tag.battleTag}} </option>
   </datalist>

    <input class="input-player2 input" type='text' v-model="player2.tag" list="player2" v-on:input="urlFunctionPlayer2()">
    <datalist id="player2" class="tag2" >
    <option v-for="tag2 in tagReturn2"> {{tag2.battleTag}} </option>
   </datalist>
   
   <br>



   <button class="button-show button" v-on:click="showRivalry"> Show</button>
   <div class="results">
      <div class="all-result">
        <span class="name-player1 big-letter"></span>
        <span class="score-player1 big-letter"></span>
        <span class="big-letter">:</span> 
        <span class="score-player2 big-letter"></span>
        <span class="name-player2 big-letter"></span>
      </div>
   </div>

  </div>
  </div>


</template>

<style scoped>

.container{
    display: flex;
    flex-direction: column;
    margin: auto;
    width: 90%;
    height:90%;
    gap:2rem;
    border: 0.1rem rgba(0,0,0, 0.25 ) solid;
    background-color: white;
    background-size:cover;
    border-radius: 0.25em;
    background-image: linear-gradient( rgba(255, 255, 255, 0.7), rgba(0, 0, 0,0.5) ),url(../assets/images/background/udhu2.jpg);
    overflow-y:auto ;
}

.title{
        color:rgb(108, 0, 151);
        font-size: 2rem;
        text-align: center;
       
    }

    .form{
        position: relative;
        display: flex;
        flex-direction: column;
        top:-1.5rem;
        
        align-items: center;
        gap:0.5rem;
        z-index: 3;
       }


      .input {
                height: 1rem;
                background-color: rgb(247, 244, 244);
                border-radius:10px;
                min-width: 15ch;
                max-width: 30ch;
                border-radius: 0.25em;
                padding: 0.25em 0.5em;
                font-size: 1rem;
               


/*                 @media (min-width: 450px) and (max-width: 750px) {
                    height: 1rem;
                    width: 9rem;
                    min-width: 10ch;
                }
                @media (max-width: 450px) {
                    min-width: 8ch;
                    height: 1rem;
                    width: 8rem;
                } */
            }

.input:hover{
                    border-color: rgb(108, 0, 151);
                    box-shadow: 0 0 15px rgb(108, 0, 151);
                    }

  .button{
            position: relative;
            width:4.5rem;
            height: 2rem;
            background-color:rgb(108, 0, 151);
            color:white; 
             border: none;
            cursor: pointer;
            border-radius: 0.25em;
            padding: 0.25em 0.5em;
            font-size: 1rem;
            cursor: pointer;
            line-height: 1.1;
  }


  .button:hover{
                background-color:rgb(108, 0, 151);
                box-shadow: 0 0 15px rgb(255, 215, 0);
            }

            .button:active {
                background-color:rgb(108, 0, 151);
                color:rgb(255, 215, 0);
            }

            .big-letter{
              color:rgb(108, 0, 151);
              font-size: 35px;
              text-shadow: 1px 1px 1px rgb(255, 255, 255);
              
            }
            .all-result{
              display: flex;
              gap:15px;
            }
</style>
