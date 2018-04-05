<template>
<div class="grid-wrapper">
        <coin v-for="(coin) in sorted_coins" v-bind:key="coin.id" :coin="coin"></coin>
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
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  grid-gap: 50px;
}
</style>
