<template>
  <div id="app">
    <h1>Amazing Crypto Joe</h1>
    <!-- <modal></modal> -->
    <div class="flexcontainer">
      <converter v-bind:coins="coins"></converter>
      <livesearch v-bind:coins="coins"></livesearch>
    </div>
    <!-- TODO: make USD in dropdown a better / working solution -->
    <modal v-bind:activeCoin="activeCoin" v-if="showCoinModal" @close="closeCoinModal">
    </modal>
    <!-- <dropdown v-if="showDropdown" @close="closeDropdown"></dropdown> -->
    <Coinlist v-bind:coins="coins"></Coinlist>
  </div>
</template>

<script>
import Coinlist from "./components/CoinList.vue";
import Modal from "./components/Modal.vue";
import Livesearch from "./components/Livesearch.vue";
import Dropdown from "./components/Dropdown.vue";
import Converter from "./components/Converter.vue";
export default {
  name: "app",
  components: { Coinlist, Modal, Livesearch, Dropdown, Converter },
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
      showCoinModal: false,
      showDropdown: true,
      activeCoin: ""
    };
  },
  created() {
    let numOfCoinsToFetch = 14;
    const url = `https://api.coinmarketcap.com/v1/ticker/?limit=${numOfCoinsToFetch}`;
    fetch(url)
      .then(response => {
        response.json().then(data => {
          this.coins = data;
        });
      })
      .catch(function(err) {
        console.log("Fetch Error :-S", err);
      });

    this.$root.$on("coinclick", data => {
      console.log("coin: ", data);
      this.activeCoin = data;
      this.showCoinModal = true;
    });
  },
  methods: {
    closeCoinModal() {
      this.showCoinModal = false;
      this.activeCoin = "";
    },
    closeDropdown() {
      this.showDropdown = false;
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
  color: #34323a;
  max-width: 1280px;
  margin: 50px auto;
}

.flexcontainer {
  display: flex;
  justify-content: space-between;
  margin: 20px;
}

.item1 {
  flex: 1 1 50%;
  display: flex;
}

h1 {
  font-size: 50px;
}
</style>
