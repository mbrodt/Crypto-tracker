<template>
  <div class="my-test">
    <div>
      <input class="my-input" v-model="amountFrom" type="text" placeholder="Amount to convert">
      <!-- <p>{{amountFrom}}</p> -->
      <select v-model="currencyFrom">
        <option value="" selected disabled hidden>Choose here</option>
        <option v-for="currency in coins" v-bind:value="currency" :key="currency.id">
          {{currency.name}} ({{currency.symbol}})
        </option>
      </select>
    </div>
    <div>
      <input class="my-input" v-model="amountTo" type="text" placeholder="Converted to">
      <select v-model="currencyTo">
        <!-- <option value="USD">US Dollars (USD)</option> -->
        <option v-for="currency in coins" v-bind:value="currency" :key="currency.id">
          {{currency.name}} ({{currency.symbol}})
        </option>
      </select>
    </div>
    <!-- <input v-model="amountTo" type="text" placeholder="Amount to convert">
        <select>
            <option value="BTC">BTC</option>
            <option value="ETH">ETH</option>
            <option value="XRP">XRP</option>
            <option value="USD">USD</option>
            <option value="EURO">EURO</option>
        </select> -->
  </div>
</template>

<script>
export default {
  props: ["coins"],
  data() {
    return {
      //   selectedOption: "",
      amountFrom: 0,
      // amountTo: 0,
      //   amountTo: 0,
      currencyFrom: {},
      currencyTo: {}
    };
  },
  computed: {
    amountTo: function() {
      console.log(
        "From: " + this.currencyFrom.name + " To: " + this.currencyTo.name
      );

      return (
        this.amountFrom *
        this.currencyFrom.price_usd /
        this.currencyTo.price_usd
      );
    }
  },
  created: function() {
    const usd = {
      name: "US Dollars",
      symbol: "USD",
      price_usd: 1
    };
    console.log("USD: " + JSON.stringify(usd));
    this.coins.push(usd);
  }
};
</script>

<style>
.my-test {
  display: flex;
  flex-wrap: wrap;
}
.my-input {
  -moz-appearance: none;
  -webkit-appearance: none;
  -webkit-box-align: center;
  -ms-flex-align: center;
  align-items: center;
  border: 1px solid transparent;
  border-radius: 3px;
  -webkit-box-shadow: none;
  box-shadow: none;
  display: -webkit-inline-box;
  display: -ms-inline-flexbox;
  display: inline-flex;
  font-size: 1rem;
  height: 2.25em;
  -webkit-box-pack: start;
  -ms-flex-pack: start;
  justify-content: flex-start;
  line-height: 1.5;
  padding-bottom: calc(0.375em - 1px);
  padding-left: calc(0.625em - 1px);
  padding-right: calc(0.625em - 1px);
  padding-top: calc(0.375em - 1px);
  position: relative;
  vertical-align: top;
  background-color: white;
  border-color: #dbdbdb;
  color: #363636;
  -webkit-box-shadow: inset 0 1px 2px rgba(10, 10, 10, 0.1);
  box-shadow: inset 0 1px 2px rgba(10, 10, 10, 0.1);
  max-width: 100%;
  width: 100px;
}

select {
  height: 100%;
  max-width: 140px;
}
</style>
