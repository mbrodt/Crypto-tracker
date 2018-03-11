<template>
<div class="modal is-active">
  <div class="modal-background"></div>
  <div class="modal-card">
    <header class="modal-card-head">
      <p class="modal-card-title">
        <!-- <slot name="header"></slot> -->
        {{ activeCoin.name }} ({{activeCoin.symbol}})
      </p>
      <button class="delete" aria-label="close" @click="$emit('close')"></button>
    </header>
    <section class="modal-card-body">
      <!-- Content ... -->
      <!-- <slot name="content"></slot> -->
      <!-- <ul> -->
      <div class="mygrid">
        <p>Price USD:</p> <p> {{activeCoin.price_usd}}$</p>
        <p>Price BTC:</p> <p> {{activeCoin.price_btc}} BTC</p>
        <p>Volume(24h):</p> <p> {{activeCoin["24h_volume_usd"]}}$</p>
        <p>Market Cap:</p> <p> {{activeCoin.market_cap_usd}}$</p>
        <p>Available Supply:</p> <p> {{activeCoin.available_supply}} {{activeCoin.symbol}}</p>
        <p>Change(1h):</p> <p> {{activeCoin.percent_change_1h}}%</p>
        <p>Change(24h):</p> <p> {{activeCoin.percent_change_24h}}%</p>
        <p>Change(7d):</p> <p> {{activeCoin.percent_change_7d}}%</p>
      </div>
      <!-- </ul> -->
      <!-- <li v-for="(value, key) in coinData" v-bind:key="key">
       {{key}} {{value }}
      </li> -->

      <!-- <p>{{activeCoin}}</p> -->

    </section>
  </div>
</div>
</template>

<script>
// import bulma from "../assets/css/bulma.css";

export default {
  props: ["activeCoin"],
  data() {
    return {
      coinData: this.activeCoin
    };
  },
  created() {}
};
</script>

<style>
.mygrid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-gap: 10px;
}
.modal-card-title {
  color: rgb(253, 243, 243);
}
.modal-card-head {
  background-color: #e76c67;
  /* background-image: linear-gradient(135deg, #43cbff 10%, #9708cc 100%); */
}

.modal-card-body {
  background-color: rgb(245, 245, 245);
}
</style>
