<template>
  <!-- <input type="text"> -->
  <!-- <div>
      <label for="search"></label>
      <input id="search" type="text">
  </div> -->
  <div class="field">
  <!-- <label class="label">Label</label> -->
  <div class="control">
    <input class="input" type="text" placeholder="Search" v-model="searchterm">
    <p> The value is {{ searchterm }}</p>
    <!-- <p> look: {{ findMatches(searchterm) }}</p> -->
    <li v-for="(coin) in findMatches(searchterm)" v-bind:key="coin.id">{{coin.name}}</li>
  </div>
  <!-- <p class="help">This is a help text</p> -->
</div>
</template>

<script>
export default {
  props: ["coins"],
  data() {
    return {
      searchterm: ""
    };
  },
  computed: {
    names: function() {
      return this.coins.map(coin => coin.name);
    }
  },
  methods: {
    findMatches: function(wordToMatch) {
      let filteredCoins = this.coins.filter(coin => {
        const regex = new RegExp(wordToMatch, "gi");
        return coin.name.match(regex);
      });
      this.$root.$emit("updated", filteredCoins);
      return filteredCoins;
    }
  }
};
</script>

<style>

</style>
