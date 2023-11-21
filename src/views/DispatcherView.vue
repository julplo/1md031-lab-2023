<template>
  <div id="orders">
    <div id="orderList">
      <div v-for="(order, key) in orders" :key="'order' + key"> 
        <span class="tjock">#{{ key }}: </span>
        <span v-if="orderItemsArray(order.orderItems).length > 0">
          {{ orderItemsString(order.orderItems) }},
        </span>
        <div>
          Skickas till: {{ order.orderNamn }} ({{ order.orderEmail }}, {{ order.orderKön }}) 
          <br>
          Betalar med: {{ order.orderPayment }}
          <br>
          <br>
        </div>
      </div>
      <button @click="clearQueue">Clear Queue</button>
    </div>
    <div id="dots" v-bind:style="{ background: 'url(' + require('../../public/img/polacks.jpg') + ')' }">
      <div v-for="(order, key) in orders" v-bind:style="{
        left: order.details.x + 'px',
        top: order.details.y + 'px'
      }" v-bind:key="'dots' + key">
        {{ key }}
      </div>
    </div>
  </div>
</template>

<script>
import io from 'socket.io-client'
const socket = io();

export default {
  name: 'DispatcherView',
  data: function () {
    return {
      orders: null
    }
  },
  created: function () {
    socket.on('currentQueue', data =>
      this.orders = data.orders);
  },
  methods: {
    orderItemsArray(orderItems) {
      const itemsArray = [];
      for (const itemName in orderItems) {
        itemsArray.push({ name: itemName, quantity: orderItems[itemName] });
      }
      return itemsArray;
    },

    orderItemsString(orderItems) {
      const itemsArray = this.orderItemsArray(orderItems);
      return itemsArray.map(item => `${item.name} x ${item.quantity}`).join(', ');
    },
    
    clearQueue: function () {
      socket.emit('clearQueue');
    },
  }
}
</script>

<style>
#orderList {
  top: 1em;
  left: 1em;
  position: absolute;
  z-index: 2;
  color: black;
  background: rgba(255, 255, 255, 0.5);
  padding: 1em;
}

#dots {
  position: relative;
  margin: 0;
  padding: 0;
  background-repeat: no-repeat;
  width: 1920px;
  height: 1078px;
  cursor: crosshair;
}

#dots div {
  position: absolute;
  background: black;
  color: white;
  border-radius: 10px;
  width: 50px;
  height: 20px;
  text-align: center;
}
  .tjock {
   font-weight: bold;
}
</style>