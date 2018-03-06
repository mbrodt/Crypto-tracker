<template>
    <div>
        <input v-model="amountFrom" type="text" placeholder="Amount to convert">
        <!-- <p>{{amountFrom}}</p> -->
        <select v-model="currencyFrom">
            <option v-for="currency in coins" v-bind:value="currency" :key="currency.id">
                {{currency.name}} ({{currency.symbol}})
            </option>
        </select>
        <input v-model="amountTo" type="text" placeholder="Converted to">
        <select v-model="currencyTo">
            <!-- <option value="USD">US Dollars (USD)</option> -->
            <option v-for="currency in coins" v-bind:value="currency" :key="currency.id">
                {{currency.name}} ({{currency.symbol}})
            </option>
        </select>
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

</style>
