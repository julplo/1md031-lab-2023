<template>
  <main>
   <header id="minheader">
       <img id="himmel" src="https://www.makelovelocks.com/wp/wp-content/uploads/2014/05/light-blue-sky-clouds-header.jpg" jsaction="VQAsE" class="sFlh5c pT0Scc iPVvYb" style="max-width: 10000px; height: 150px; margin: 8.5px 0px; width: 10000x;" alt="light-blue-sky-clouds-header - MakeLoveLocks.com" jsname="kn3ccd" aria-hidden="false">
       <div class="header-text">
           <h1>Välkommen till BurgerHeaven Online</h1>
       </div>
   </header>

  <section id="väljaburgare">
      <br>
    <label class="tjock" for="väljaburgare">Välja burgare!</label><br>
      <br>
      Här väljer du din burgare.
      <br>
    <div> 
      <Burger v-for="burger in burgers"
          v-bind:burger="burger" 
          v-bind:key="burger.name"
            v-on:orderedBurgers="addToOrder($event)"/>
    </div>
</section>

  <section id="contact">
<br>
 <label class="tjock" for="contact">Dina uppgifter</label><br>
  
<form>
  <div>
      <p>
    <label  for="Namn">Namn</label><br>
    <input v-model="namn" placeholder="För- och efternamn" />
     </p>
      <p>
    <label for="Email">Email adress</label><br>
    <input v-model="email" placeholder="Namn@exempel.com" />
      </p>
      <p>
      <label for="payment">Betalsätt</label><br>
    <select v-model="payment">
        <option>Faktura</option>
        <option>Swish</option>
        <option>Kort</option>
        <option>Klarna</option>
    </select>
    </p>
  </div>

    <label class="tjock" for="map-container">Leverans</label><br> 
    <br>
    <label for="map">Välj vart vi ska skicka din beställnig</label><br> 
      <div id="map-container">   
        <div id="map" v-on:click="setLocation" v-bind:style="{ position: 'relative' }">
          <div v-bind:style="{ position: 'absolute', left: location.x + 'px', top: location.y + 'px' }"
                style="color: red; font-weight: bold;">
            HÄR!
      </div>
    </div> 
    </div>

    <div>
      <p> 
      <label class="tjock" for="kön">Kön</label><br>
        
      <input type="radio" id="kvinna" v-model="kön" value="kvinna">
        <label for="kvinna">Kvinna</label>
        <br>
      <input type="radio" id="Man" v-model="kön" value="man">
        <label for="Man">Man</label>
        <br>
      <input type="radio" id="Annat" v-model="kön" value="Annat">
        <label for="Annat">Annat</label>
        <br>
      <input type="radio" id="VillInteSäga" v-model="kön" value="Vill inte säga">
        <label for="VillInteSäga">Vill inte säga</label>
        <br>
      </p>
    </div>

</form>
           </section>

           <section>
               <button type="submit" class="custom-button" v-on:click="sendInfo">
                   <img src="https://static.vecteezy.com/ti/gratis-vektor/p3/3667144-isolerad-valsmakande-stor-hamburgare-pa-vit-bakgrund-platt-design-tecknad-burger-med-ost-och-sesamfron-isolerade-pa-vit-bakgrund-vektor-illustration-vector.jpg" jsaction="VQAsE" class="sFlh5c pT0Scc iPVvYb" style="max-width: 20px; width: 20px; height: 20px; margin: 0px;" alt="isolerade välsmakande stor hamburgare på vit bakgrund. platt ..." jsname="kn3ccd">
                   Beställ!
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
import menu from '../assets/menu.json'
import Burger from '../components/OneBurger.vue'
import io from 'socket.io-client'

const socket = io();

/*function MenuItem(name, imageUrl, kCal, containsGluten, containsLactose) {
 this.name = name;
 this.imageUrl = imageUrl;
 this.kCal = kCal;
 this.containsGluten = containsGluten;
 this.containsLactose = containsLactose;
}

const theburgers = [
 new MenuItem("Klassikern", "https://www.sweetbabyrays.se/lidd/content/images/Grillad-hamburgare-med-BBQ-sas.jpg", 750, true, true),
 new MenuItem("Veggie","https://res.cloudinary.com/coopsverige/image/upload/f_auto,fl_progressive,q_90,g_center,h_800,w_800/v1545220329/358025.jpg", 600, false, false ),
 new MenuItem("BBQ burgare", "https://res.cloudinary.com/coopsverige/image/upload/f_auto,fl_progressive,q_90,g_center,h_800,w_800/v1521205971/281117.jpg", 700, true, false)

]
console.log(theburgers); /* printa till consolen */

export default {
  name: 'HomeView',
  components: {
    Burger
  },
  data() {
    return {
      burgers: menu,
    
      namn: '', 
      email:'',
      gata: '',
      hus: '', 
      payment: 'Kort', 
      kön: '',

      orderedBurgers: {}, 

      location: {x:0, y:0}
    }
  },
 methods: {
  sendInfo() {
      console.log('Namn:', this.namn);
      console.log('Email:', this.email);
      console.log('Payment:', this.payment);
      console.log('Kön:', this.kön);

      console.log('Ordered Burgers', this.orderedBurgers)

      console.log('Location', this.location)

      socket.emit("addOrder", {
        orderId: this.getOrderNumber(),
        details: this.location,
        orderItems: this.orderedBurgers,
        orderNamn: this.namn,
        orderEmail: this.email,
        orderKön: this.kön,
        orderPayment: this.payment
      });
  },
   
  
   getOrderNumber: function () {
     return Math.floor(Math.random()*1000);
   },

   addToOrder: function (event) {
  this.orderedBurgers[event.name] = event.amount;
  console.log(`Ordered ${event.amount} of ${event.name}`);
  
},

setLocation(event) {
      const offset = {
        x: event.currentTarget.getBoundingClientRect().left,
        y: event.currentTarget.getBoundingClientRect().top
      };

      this.location = {
        x: event.clientX - 10 - offset.x,
        y: event.clientY - 10 - offset.y
      };
    },

    addOrder(event) {
      this.setLocation(event);
    }
  }
}

</script>

<style>

 body {
   font-family: 'Georgia', serif;
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

#map-container {
  width: 800px; 
  height: 400px; 
  overflow: scroll;
  border: 2px solid black; 
}

#map {
  width: 1920px;
  height: 1078px;
  background: url("https://raw.githubusercontent.com/julplo/1md031-lab-2023/main/public/img/polacks.jpg");
}

</style>