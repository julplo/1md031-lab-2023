<template>
  <div class="burger-item">
    <img :src="burger.imageUrl" alt="Burger Image" class="burger-image" />
    <div class="burger-info">
      <h2>{{ burger.name }}</h2>
      <ul>
        <li>{{ burger.kCal }} kCal</li>
        <li>Innehåller gluten: {{ burger.containsGluten ? 'Ja' : 'Nej' }}</li>
        <li>Innehåller laktos: {{ burger.containsLactose ? 'Ja' : 'Nej' }}</li>
      </ul>
      <button v-on:click="increaseBurgers">+</button>
      {{ amountOrdered }}
      <button v-on:click="decreaseBurgers">-</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'OneBurger',
  props: {
    burger: Object
  },
  data() {
    return {
      amountOrdered: 0,
    };
  },
  methods: {
    increaseBurgers() {
      this.amountOrdered++;
      this.$emit('orderedBurgers', { 
        name: this.burger.name, 
        amount: this.amountOrdered 
      });
    },
    decreaseBurgers() {
      if (this.amountOrdered > 0) {
        this.amountOrdered--;
        this.$emit('orderedBurgers', { 
        name: this.burger.name, 
        amount: this.amountOrdered 
      });
      }
    },
    addBurger() {
      this.amountOrdered += 1;
      this.$emit('orderedBurgers', { 
        name: this.burger.name, 
        amount: this.amountOrdered 
      });
    },
  }
};
</script>

<style scoped>
body {
  font-family: 'Georgia', 'Times New Roman', serif;
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

.burger-item {
  display: inline-block; /* hamburgarna visas i en rad */
  width: 200px;
  margin: 20px;
}

.burger-image {
  width: 100%;
  height: auto;
  border-radius: 10px;
}
</style>