<template>
  <div id="app">
    <h1>Amazing Crypto Joe</h1>
    <!-- <modal></modal> -->
    <modal v-if="showCoinModal" @close="showCoinModal = false" ></modal>
    <button @click="showCoinModal = true" >Show modal</button>
    <livesearch v-bind:coins="coins"></livesearch>
  <Coinlist v-bind:coins="coins"></Coinlist>
  </div> 
</template>

<script>
import Coinlist from "./components/CoinList.vue";
import Modal from "./components/Modal.vue";
import Livesearch from "./components/Livesearch.vue";
export default {
  name: "app",
  components: { Coinlist, Modal, Livesearch },
  data() {
    return {
      coins: [
        {
          name: "BTC",
          price_usd: "100"
        },
        {
          name: "LOL",
          price_usd: "50"
        },
        {
          name: "ETH",
          price_usd: "20"
        },
        {
          name: "LTC",
          price_usd: "10"
        },
        {
          name: "RIP",
          price_usd: "5"
        }
      ],
      showCoinModal: false
    };
  },
  created() {
    let numOfCoinsToFetch = 10;
    const url = `https://api.coinmarketcap.com/v1/ticker/?limit=${numOfCoinsToFetch}`;
    fetch(url)
      .then(response => {
        response.json().then(data => {
          console.log(data);
          this.coins = data;
        });
      })
      .catch(function(err) {
        console.log("Fetch Error :-S", err);
      });
    this.$root.$on("coinclick", data => {
      console.log("hey");
      // console.log(data);
    });
  },
  methods: {
    updateModal() {
      alert("heard");
    }
  },
  computed: {
    euro_prices: function() {
      const euro_prices = this.coins.map(x => (x.price_usd * 0.83).toFixed(3));
      return euro_prices;
    }
  }
};
</script>

<style>
@import "assets/css/bulma.css";
</style>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
