
<script lang="ts">



export default{

  data() {
    return {
     player1:{
      tag:"iNSUPERABLE#11842",
     },
     player2:{
      tag:"РозовыйПони#228941",
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
  let winrate1:any = document.querySelector('.winrate1');
let winrate2:any = document.querySelector('.winrate2');

if((this.score1 +this.score2)!=0) {
winrate1.innerHTML =  Math.round((100*this.score1)/ (this.score1 +this.score2)) +'%';
winrate2.innerHTML =  Math.round((100*this.score2)/ (this.score1 +this.score2)) + '%';
}

else{
  winrate1.innerHTML=0+'%';
  winrate2.innerHTML=0+'%';
}
this.score1=0;
this.score2=0;
/*   console.log(this.score1, this.score2); */
},


async showRivalryByRaces (race1:any,race2:any) {
   
let player1score:any=0;
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

 
 }

 switch (race1) {
    case 0:  race1= 'XR';
   
    break;

  case 1:  race1= 'H';
   
  break;

  case 2:  race1= 'O';
   
  break;

  case 4:  race1= 'N';
   
   break;

   case 8:  race1= 'U';
   
   break;

  default:

  break;
   } 

   switch (race2) {
    case 0:  race2= 'XR';
   
    break;

  case 1:  race2= 'H';
   
  break;

  case 2:  race2= 'O';
   
  break;

  case 4:  race2= 'N';
   
   break;

   case 8:  race2= 'U';
   
   break;

  default:

  break;
   } 


   //count winrate
   let percent1:any=0;
   let percent2:any=0;

   if((player1score +player2score)!=0) {
   percent1 = Math.round((100 * player1score)/ (player1score + player2score))+'%';
   percent2 = Math.round((100 * player2score)/ (player1score + player2score))+'%';
   }

   else {
    percent1=0+'%';
    percent2=0+'%';
   }
 
this.raceArray.shift;

if(player1score!=0 || player2score!=0){
 this.raceArray.push(race1,percent1,player1score,player2score,percent2, race2);
}

//from big array to smallest arrays 6size
function sliceIntoChunks(arr:any, chunkSize:any) {
    const res = [];
    for (let i = 0; i < arr.length; i += chunkSize) {
        const chunk = arr.slice(i, i + chunkSize);
        res.push(chunk);
    }
    return res;
}



this.raceArray1 = sliceIntoChunks(this.raceArray, 6);
//sort array

this.raceArray1.sort();

// split array to 5 arrays

this.raceArray1=sliceIntoChunks(this.raceArray1, 5);

/* console.log(this.raceArray1); */

setTimeout(() => {
  this.changeIcons();
}, 1000);




},
changeIcons (){


 
  console.log('callback')
  
let icons=document.querySelectorAll('.race-column');
icons.forEach(element => {

  if(element.innerHTML=="H"){
    element.innerHTML = `<img src="/src/assets/images/icons/human-icon-small.svg" alt="human">`;
  }
  if(element.innerHTML=="O"){
    element.innerHTML = `<img src="/src/assets/images/icons/orc-icon-small.svg" alt="orc">`;
  }
  if(element.innerHTML=="U"){
    element.innerHTML = `<img src="/src/assets/images/icons/undead-icon-small.svg" alt="undead">`;
  }
  if(element.innerHTML=="N"){
    element.innerHTML = `<img src="/src/assets/images/icons/nightelf-icon-small.svg" alt="elf">`;
  }
  if(element.innerHTML=="XR"){
    element.innerHTML = `<img src="/src/assets/images/icons/random-icon-small.svg" alt="random">`;
  } 
    
}
);


},
showAll (){

  this.showRivalryByRaces (this.orc,this.human)
  this.showRivalryByRaces (this.orc,this.orc)
  this.showRivalryByRaces (this.orc,this.elf)
  this.showRivalryByRaces (this.orc,this.undead)
  this.showRivalryByRaces (this.orc,this.rnd)
  this.showRivalryByRaces (this.human,this.human)
  this.showRivalryByRaces (this.human,this.orc)
  this.showRivalryByRaces (this.human,this.elf)
  this.showRivalryByRaces (this.human,this.undead)
  this.showRivalryByRaces (this.human,this.rnd)
  this.showRivalryByRaces (this.elf,this.human)
  this.showRivalryByRaces (this.elf,this.orc)
  this.showRivalryByRaces (this.elf,this.elf)
  this.showRivalryByRaces (this.elf,this.undead)
  this.showRivalryByRaces (this.elf,this.rnd)
  this.showRivalryByRaces (this.undead,this.human)
  this.showRivalryByRaces (this.undead,this.orc)
  this.showRivalryByRaces (this.undead,this.elf)
  this.showRivalryByRaces (this.undead,this.undead)
  this.showRivalryByRaces (this.undead,this.rnd)
  this.showRivalryByRaces (this.rnd,this.human)
  this.showRivalryByRaces (this.rnd,this.orc)
  this.showRivalryByRaces (this.rnd,this.elf)
  this.showRivalryByRaces (this.rnd,this.undead)
  this.showRivalryByRaces (this.rnd,this.rnd)
 
  this.raceArray=[];
},
showPanel() {
  let results = document.querySelector('.results');

  results?.classList.add('active');

},
 changeInput (){
  let player1 = this.player1.tag;
  let player2 = this.player2.tag;
  this.player1.tag= player2;
  this.player2.tag= player1;

},


},


}


</script>


<template>
  
  <div class="container">
    <div class="title"> W3Champions Rivalry Counter </div>
    
    <div class="form">

    <input class="input-player1 input" type='text' v-model="player1.tag" list="player1" v-on:input="urlFunctionPlayer1()">
    <datalist id="player1" class="tag" >
    <option v-for="tag in tagReturn" v-bind:key="tag"> {{tag.battleTag}} </option>
   </datalist>
   
   <img  class="test1" src="../assets/images/icons/orc-icon-small.svg" alt="human">
   <img  class="test1" src="../assets/images/icons/human-icon-small.svg" alt="human">
   <img  class="test1" src="../assets/images/icons/undead-icon-small.svg" alt="human">
   <img  class="test1" src="../assets/images/icons/nightelf-icon-small.svg" alt="human">
   <img  class="test1" src="../assets/images/icons/random-icon-small.svg" alt="human">

    <input class="input-player2 input" type='text' v-model="player2.tag" list="player2" v-on:input="urlFunctionPlayer2()">
    <datalist id="player2" class="tag2" >
    <option v-for="tag2 in tagReturn2" v-bind:key="tag2"> {{tag2.battleTag}} </option>
   </datalist>
   <div class="arrows" v-on:click="changeInput()"></div>
   



   <button class="button-show button" v-on:click="showRivalry(); showAll(); showPanel();"> Show</button>

   <div class="results">
      <div class="big-result">
        <span class="winrate1 big-letter"></span>
        <span class="name-player1 big-letter"></span>
        <span class="score-player1 big-letter"></span>
        <span class="big-letter">:</span> 
        <span class="score-player2 big-letter"></span>
        <span class="name-player2 big-letter"></span>
        <span class="winrate2 big-letter"></span>
      </div>
      <div class="all-results">
        <div class='matchup' v-for="bigItem in raceArray1" v-bind:key="bigItem"> 
  <div class='all-score' v-for="item in bigItem" v-bind:key="item">
        <span class="left-column">
         <span class="info percent-column">{{item[1] }}</span> 
         <span class="info race-column">{{item[0]}}</span> 
         <span class="info score-column">{{item[2]}}</span>
        </span>
         <span class="colon">:</span>
         <span class="right-column">
          <span class="info score-column">{{item[3]}}</span>
          <span class="race-column info">{{item[5]}}</span>
          <span class="info percent-column">{{item[4]}}</span>
        </span>
        </div>
       </div>          
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

            }

            .arrows{
              position: relative;
              width:30px;
              height: 30px;
              cursor: pointer;
              top:-55px;
              left: 130px;
              background-image: url(../assets/images/arrows.png);
              background-size:cover;
                                      
            }

            .arrows:hover{
              background-image: url(../assets/images/arrows_hover.png);
            
            }
.input:hover{
                    border-color: rgb(108, 0, 151);
                    box-shadow: 0 0 15px rgb(108, 0, 151);
                    
                    }

  .button{

            position: relative;
            top:-20px;
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
                box-shadow: 0 0 15px rgb(241, 241, 241);
            }

            .button:active {
                background-color:rgb(108, 0, 151);
                color:rgb(255, 215, 0);
            }

            .big-letter{
              color:rgb(108, 0, 151);
              font-size: 35px;
              text-shadow: 1px 1px 1px rgb(255, 255, 255);
              margin: auto;
              
            }

/*             .score-player2{
              
              
           
            }

            .score-player1{
              
      
            } */


            .results{
            display: none;
            }
            .active{
            display: block;
            width: 95%;
          
            }
            .big-result{
              display: flex;
              gap:15px;
              background-color: rgba(255, 255, 255, 0.452);
              flex-wrap: wrap;
            }


            .all-results{
              display: flex;
              flex-direction: row;
              gap:10px;
              position: relative;
              top:25%;
              flex-wrap: wrap;
              justify-content: space-around;
              
            }
            .matchup{
              display: flex;
              background-color: rgba(255, 255, 255, 0.452);
              flex-wrap: wrap;
              flex-direction: column;
              width:210px;
              font-size: 20px;
              gap:5px;
              
            }

            .all-score{
              display: flex;
              gap:5px;
             
             
            }

            .colon{
                margin: auto;
            }

            .info{
              color:rgb(108, 0, 151);
              
            }
            .left-column{
              display: flex;
             
              width:90px;
              justify-content: space-between;
              

            }

            .right-column{
              display: flex;
              
              width:90px;
              justify-content: space-between;
              
              
              
            }

            .percent-column{
              position: relative;
              width: 47px;
              text-align: center;
             /*  background-color: green; */
              
            }


            
            .score-column {
             /*  background-color: yellow; */
              width:18px;
              text-align: center;
            }

            @media (min-width: 650px) and (max-width: 870px) {
              .big-letter{
              
              font-size: 25px;
            }


            }

            @media (min-width: 550px) and (max-width: 649px) {
              .big-letter{
              
              font-size: 20px;
            }
            }

            @media (min-width: 400px) and (max-width: 549px) {
              .big-letter{
              
              font-size: 20px;
            }
            .big-result{
              display: flex;
              gap:1px;
            }
            .winrate1{
             display: none;
        
            }

            .winrate2{
              display: none;
            }

            .all-results{

              top:15%;

              }
            }
            @media (max-width: 399px) {
              .big-letter{
              
              font-size: 17px;
            }
            .big-result{
              display: flex;
              gap:1px;
            }
            .winrate1{
             display: none;
        
            }

            .winrate2{
              display: none;
            }

            .score-player1{
              font-size: 20px;
             
            }

            .score-player2{
              font-size: 20px;
            }

            .all-results{

              top:5%;

              }
              .arrows{
                top:-50px;
              width: 25px;
              height: 25px;
              left: 125px;
            }
            }

.test1{
      /* background-image: url(../assets/images/logo.png); */
      width:15px;
      height: 15px;
}



</style>
