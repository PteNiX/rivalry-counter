
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
     orc:2,
     human:1,
     elf:4,
     undead:8,
     rnd:0,
     player1score:0,
     player2score:0,

     scoreHO1:0,
     scoreHO2:0,
     scoreHH1:0,
     scoreHH2:0,
     scoreHU1:0,
     scoreHU2:0,
     scoreHE1:0,
     scoreHE2:0,
     scoreHR1:0,
     scoreHR2:0,
     scoreOH1:0,
     scoreOH2:0,
     scoreOO1:0,
     scoreOO2:0,
     scoreOU1:0,
     scoreOU2:0,
     scoreOE1:0,
     scoreOE2:0,
     scoreOR1:0,
     scoreOR2:0,
     scoreEO1:0,
     scoreEO2:0,
     scoreEH1:0,
     scoreEH2:0,
     scoreEU1:0,
     scoreEU2:0,
     scoreEE1:0,
     scoreEE2:0,
     scoreER1:0,
     scoreER2:0,
     scoreUO1:0,
     scoreUO2:0,
     scoreUH1:0,
     scoreUH2:0,
     scoreUE1:0,
     scoreUE2:0,
     scoreUU1:0,
     scoreUU2:0,
     scoreUR1:0,
     scoreUR2:0,
     scoreRO1:0,
     scoreRO2:0,
     scoreRH1:0,
     scoreRH2:0,
     scoreRU1:0,
     scoreRU2:0,
     scoreRE1:0,
     scoreRE2:0,
     scoreRR1:0,
     scoreRR2:0,

     raceArray:[1],
     raceArray1:[1],
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

  /* console.log (dataScore); */
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
/*   console.log(this.score1, this.score2); */
},


async showRivalryByRaces (race1:number,race2:number,var1:any, var2:any) {
   
let player1score=0;
let player2score=0;
   for(let i=2; i<15; i++) {
  
 this.urlGames1 =`https://website-backend.w3champions.com/api/matches/search?playerId=${this.player1.tag.trim().replace('#', '%23')}&gateway=20&offset=0&opponentId=${this.player2.tag.trim().replace('#', '%23')}&pageSize=50&season=${i}&gamemode=1`;
 
 const resScore  = await fetch(this.urlGames1);
 const dataScore  = await resScore.json();



   for (let i = 0; i < dataScore.matches.length; i++) {
     if (
       dataScore.matches[i].teams[0].players[0].battleTag == `${this.player1.tag.trim()}` &&
       dataScore.matches[i].teams[0].won == true &&
       dataScore.matches[i].teams[0].players[0].race == `${race1}` &&
       dataScore.matches[i].teams[1].players[0].race == `${race2}`

     ) {
      player1score++;
     }
       else if (
       dataScore.matches[i].teams[0].players[0].battleTag == `${this.player1.tag.trim()}` &&
       dataScore.matches[i].teams[0].won == false &&
       dataScore.matches[i].teams[0].players[0].race == `${race1}` &&
       dataScore.matches[i].teams[1].players[0].race == `${race2}`

       ){
        player2score++;
       }
   
     if (
       dataScore.matches[i].teams[1].players[0].battleTag == `${this.player1.tag.trim()}`  &&
       dataScore.matches[i].teams[1].won == true &&
       dataScore.matches[i].teams[0].players[0].race == `${race2}` &&
       dataScore.matches[i].teams[1].players[0].race == `${race1}`
     ) {
      player1score++;
     }
     else if (dataScore.matches[i].teams[1].players[0].battleTag == `${this.player1.tag.trim()}` &&
       dataScore.matches[i].teams[1].won == false &&
       dataScore.matches[i].teams[0].players[0].race == `${race2}` &&
       dataScore.matches[i].teams[1].players[0].race == `${race1}`){
        player2score++;
        
       }

      
   }





  /* console.log(this.scoreOH1,this.scoreOH2,this.scoreOO1,this.scoreOO2,this.scoreOE1,this.scoreOE2,this.scoreOU1,this.scoreOU2,this.scoreOR1,this.scoreOR2,this.scoreUR1, this.scoreUR2,this.scoreUU1, this.scoreUU2,this.scoreUE1, this.scoreUE2, this.scoreUO1, this.scoreUO2,this.scoreUH1, this.scoreUH2 ) */
  /*  this.raceArray=raceArray; */

 }
this.raceArray.shift;
 this.raceArray.push(player1score,player2score);
 console.log(this.raceArray)



},
showAll (){
  this.showRivalryByRaces (this.orc,this.human, this.scoreOH1,this.scoreOH2)
  this.showRivalryByRaces (this.orc,this.orc,this.scoreOO1,this.scoreOO2)
  this.showRivalryByRaces (this.orc,this.elf,this.scoreOE1,this.scoreOE2)
  this.showRivalryByRaces (this.orc,this.undead, this.scoreOU1,this.scoreOU2)
  this.showRivalryByRaces (this.orc,this.rnd,this.scoreOR1,this.scoreOR2 )
  this.showRivalryByRaces (this.human,this.human, this.scoreHH1,this.scoreHH2 )
  this.showRivalryByRaces (this.human,this.orc, this.scoreHO1,this.scoreHO2)
  this.showRivalryByRaces (this.human,this.elf, this.scoreHE1,this.scoreHE2)
  this.showRivalryByRaces (this.human,this.undead, this.scoreHU1,this.scoreHU2)
  this.showRivalryByRaces (this.human,this.rnd, this.scoreHR1,this.scoreHR2)
  this.showRivalryByRaces (this.elf,this.human, this.scoreEH1,this.scoreEH2)
  this.showRivalryByRaces (this.elf,this.orc,this.scoreEO1,this.scoreEO2)
  this.showRivalryByRaces (this.elf,this.elf, this.scoreEE1,this.scoreEE2)
  this.showRivalryByRaces (this.elf,this.undead, this.scoreEU1,this.scoreEU2)
  this.showRivalryByRaces (this.elf,this.rnd, this.scoreER1,this.scoreER2)
  this.showRivalryByRaces (this.undead,this.human, this.scoreUH1, this.scoreUH2)
  this.showRivalryByRaces (this.undead,this.orc, this.scoreUO1, this.scoreUO2)
  this.showRivalryByRaces (this.undead,this.elf, this.scoreUE1, this.scoreUE2)
  this.showRivalryByRaces (this.undead,this.undead, this.scoreUU1, this.scoreUU2)
  this.showRivalryByRaces (this.undead,this.rnd, this.scoreUR1, this.scoreUR2)
  this.showRivalryByRaces (this.rnd,this.human, this.scoreRH1, this.scoreRH2)
  this.showRivalryByRaces (this.rnd,this.orc, this.scoreRO1, this.scoreRO2)
  this.showRivalryByRaces (this.rnd,this.elf, this.scoreRE1, this.scoreRE2)
  this.showRivalryByRaces (this.rnd,this.undead, this.scoreRU1, this.scoreRU2)
  this.showRivalryByRaces (this.rnd,this.rnd, this.scoreRR1, this.scoreRR2)
/* console.log(this.scoreOH1,this.scoreOH2,this.scoreOO1,this.scoreOO2,this.scoreOE1,this.scoreOE2,this.scoreOU1,this.scoreOU2,this.scoreOR1,this.scoreOR2,this.scoreUR1, this.scoreUR2,this.scoreUU1, this.scoreUU2,this.scoreUE1, this.scoreUE2, this.scoreUO1, this.scoreUO2,this.scoreUH1, this.scoreUH2 ) */
 
  this.raceArray=[];
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



   <button class="button-show button" v-on:click="showRivalry(); showAll()"> Show</button>
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
