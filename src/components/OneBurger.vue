<template>
  <div class="wrapper">
     <h1>{{ burger.name }}</h1>
     <img v-bind:src="burger.imageUrl">
     <ul>
       <li>{{ burger.kCal }} kCal</li>
       <li>Contains Gluten: {{ burger.containsGluten ? 'Yes' : 'No' }}</li>
       <li>Contains Lactose: {{ burger.containsLactose ? 'Yes' : 'No' }}</li>
     </ul>
   </div>
 </template>
   
   <script>
   export default {
     name: 'OneBurger',
     props: {
       burger: Object
     }
   }
   </script>
   
   <!-- Add "scoped" attribute to limit CSS to this component only -->
   <style scoped>
  body {
     font-family: 'Georgia', 'Times New Roman', serif;
 }
 
 .tjock {
     font-weight: bold;
 }
 
 #minheader {
     position: relative;
 }
 
 #minheader .header-text {
     position: absolute;
     top: 50%;
     left: 50%;
     transform: translate(-50%, -50%);
     text-align: center;
     color: darkblue;
     margin-top: -1;
     font-size: 1.3em;
     white-space: nowrap;
 }
 
 @media screen and (max-width: 800px) {
     h1 {
         font-size: 6vw;
     }
 }
 
 #väljaburgare {
     background-color: black;
     color: white;
     padding: 0.2em 0.7em;
     border-radius: 25px;
     border: dashed white;
 }
 
 .wrapper {
     display: grid;
     grid-gap: 10px;
     grid-template-columns: 300px 300px 300px;
     text-align: center;
 }
 
 .box {
     padding: 15px;
     margin: 10px;
 }
   </style>
   
  