<template>
  <div id="app">
      <!--
    <img alt="Vue logo" src="./assets/logo.png">
      <h1>Number Alpha: {{alpha}}</h1>
      <HelloWorld msg="Welcome to Your Vue.js App"/>
      
      <button v-on:click="increaseAlpha">Click</button>
      -->

      <h2>{{ loadStateTitle }}</h2>
      
      <div v-for="(o, index) in titles">
        <h2>{{ o.title }}</h2> <h4>({{ (new Date(o.startDate)).toLocaleDateString() }})</h4>

        <h1 v-if="o.title.match( /Hafven/ )" >Intern</h1>
      </div>

  </div>
  
</template>


<script>

//import HelloWorld from './components/HelloWorld.vue'

import axios from 'axios';

export default {

  name: 'app',

  components: {
//    HelloWorld
  },

  data : () => {

return {

loadStateTitle : "Loading...",

alpha : 123,

hafvenCalendar : {},

titles : [],

};

    },

methods : {

increaseAlpha()
{
     this.alpha++;
}


} ,



created : function(){

  axios.get( 'https://cors.io/?https://hafven.de/programmkalendar/?format=json' ).then(

   (res) => {

     this.loadStateTitle = "";

     console.log( "hafven dump: ", res.request.response );

     this.hafvenCalendar = JSON.parse(res.request.response);

      for( let index in this.hafvenCalendar.upcoming )
      {
         const obj = this.hafvenCalendar.upcoming[index];

         this.titles.push( { title : obj.title, startDate  : obj.startDate } );
      }
   }

);


}



};



</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
