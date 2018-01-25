<template>
<div class="grid-wrapper">
        <coin v-for="(coin, i) in sorted_coins" v-bind:key="coin.id"  > 
          {{coin.name}}
            <br>
             {{coin.price_usd}}$
             <br>
             {{euro_prices[i]}}€
             </coin>
</div>
  
</template>

<script>
import Coin from "./Coin.vue";
export default {
  props: ["coins"], //Get coins from parent
  data() {
    return {
      sorted_coins: this.coins
    };
  },
  components: { Coin },
  methods: {},
  computed: {
    euro_prices: function() {
      const euro_prices = this.coins.map(x => (x.price_usd * 0.83).toFixed(3));
      return euro_prices;
    }
  },
  mounted() {
    this.$root.$on("updated", data => {
      console.log(data);
      this.sorted_coins = data;
    });
  }
};
</script>

<style>
.grid-wrapper {
  list-style-type: none;
  display: grid;
  /* grid-template-columns: repeat(3, 1fr); */
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  grid-gap: 50px;
  justify-content: start;
  align-content: start;
}
</style>
