<template>
  <main>
   <header id="minheader">
       <img id="himmel" src="https://www.makelovelocks.com/wp/wp-content/uploads/2014/05/light-blue-sky-clouds-header.jpg" jsaction="VQAsE" class="sFlh5c pT0Scc iPVvYb" style="max-width: 10000px; height: 150px; margin: 8.5px 0px; width: 10000x;" alt="light-blue-sky-clouds-header - MakeLoveLocks.com" jsname="kn3ccd" aria-hidden="false">
       <div class="header-text">
           <h1>Välkommen till BurgerHeaven Online</h1>
       </div>
   </header>

   <section id="väljaburgare">
     <h1>Välja burgare!</h1>
     Här väljer du din burgare.
     <br>

     <div class="wrapper">
       <burger v-for="(burger, index) in burgers" :key="index" :burger="burger" />
     </div>
   </section>

       <section id="contact">
           <h1>Dina uppgifter:</h1>
           <form>
               <p>
                   <label for="name">Namn</label><br>
                   <input type="text" id="name" name="fn" required="required" placeholder="För- och efternamn">
               </p>
               <p>
                   <label  for="email">Email adress</label><br>
                   <input type="email" id="email" name="em" required="required" placeholder="E-mail adress">
               </p>
               <p>
                   <label for="street">Gata</label><br>
                   <input type="text" id="street" name="ln" placeholder="Gatunamn">
               </p>
               <p>
                   <label for="hus">Hus</label><br>
                   <input type="number" id="hus" name="ln" placeholder="Husnummer">
               </p>
               <p>
                   <label class="tjock" for="payment">Betalsätt</label><br>
                   <select id="payment" name="payment">
                       <option>Faktura</option>
                       <option>Swish</option>
                       <option selected="selected">Kort</option>
                       <option>Klarna</option>
                   </select>
               </p>
               <p>
               <label class="tjock" for="gender">Kön</label><br>

                   <input type="radio" id="kvinna" name="gender" value="kvinna">
                   <label for="kvinna">Kvinna</label><br>
                   <input type="radio" id="man" name="gender" value="man">
                   <label for="man">Man</label><br>
                   <input type="radio" id="ickebinar" name="gender" value="icke-binär">
                   <label for="ickebinar">Icke-binär</label><br>
                   <input checked="checked" type="radio" id="annat" name="gender" value="annat">
                   <label for="annat">Annat</label><br> 

               </p>
               </form>
           </section>

           <section>
               <button type="submit" class="custom-button">
                   <img src="https://static.vecteezy.com/ti/gratis-vektor/p3/3667144-isolerad-valsmakande-stor-hamburgare-pa-vit-bakgrund-platt-design-tecknad-burger-med-ost-och-sesamfron-isolerade-pa-vit-bakgrund-vektor-illustration-vector.jpg" jsaction="VQAsE" class="sFlh5c pT0Scc iPVvYb" style="max-width: 20px; width: 20px; height: 20px; margin: 0px;" alt="isolerade välsmakande stor hamburgare på vit bakgrund. platt ..." jsname="kn3ccd">
                   Send Info
                 </button>
           </section>

           <section>
               <h1>Kontakta oss!</h1>
               Ring 123 456 789
               <br>
               <br>
           </section>
   </main>

   <hr>
   <footer>
       &copy; 2023 BestBurgersEver | All rights reserved
   </footer>
</template>

<script>
import Burger from '../components/OneBurger.vue'
import io from 'socket.io-client'

const socket = io();

function MenuItem(name, imageUrl, kCal, containsGluten, containsLactose) {
 this.name = name;
 this.imageUrl = imageUrl;
 this.kCal = kCal;
 this.containsGluten = containsGluten;
 this.containsLactose = containsLactose;
}

const theburgers = [
 new MenuItem("Klassikern", "https://www.sweetbabyrays.se/lidd/content/images/Grillad-hamburgare-med-BBQ-sas.jpg", 700, true, true),
 new MenuItem("Veggie","https://res.cloudinary.com/coopsverige/image/upload/f_auto,fl_progressive,q_90,g_center,h_800,w_800/v1545220329/358025.jpg", 700, false, false ),
 new MenuItem("BBQ burgare", "https://res.cloudinary.com/coopsverige/image/upload/f_auto,fl_progressive,q_90,g_center,h_800,w_800/v1521205971/281117.jpg", 700, true, false)

];

console.log(theburgers); /* printa till consolen */

export default {
 name: 'HomeView',
 components: {
   Burger
 },
 data: function () {
   return {
     burgers: theburgers
   }
 },
 methods: {
   getOrderNumber: function () {
     return Math.floor(Math.random()*100000);
   },
   addOrder: function (event) {
     var offset = {x: event.currentTarget.getBoundingClientRect().left,
                   y: event.currentTarget.getBoundingClientRect().top};
     socket.emit("addOrder", { orderId: this.getOrderNumber(),
                               details: { x: event.clientX - 10 - offset.x,
                                          y: event.clientY - 10 - offset.y },
                               orderItems: ["Beans", "Curry"]
                             }
                );
   }
 }
}
</script>

<style>

 body {
   font-family: 'Georgia', 'Times New Roman', serif;
}

.tjock {
   font-weight: bold;
}

#stort {
   text-transform: uppercase;
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

#himmel {
   opacity: 0.7;
   width: 100%;
   height: auto;
}

#väljaburgare {
   background-color: black;
   color: white;
   padding: 0.2em 0.7em;
   border-radius: 25px;
   border: dashed white;
}

#contact {
   padding: 0.2em 0.7em;
   margin-top: 0.5em; 
   border-radius: 25px;
   border: dashed black;
}

button:hover {
   background-color: darkblue;
}

.custom-button {
   cursor: pointer;
   margin: 0.7em;
   margin-top: 2em;
   background-color: lightblue;
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