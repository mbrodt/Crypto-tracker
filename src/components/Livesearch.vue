<template>
  <div class="field">
  <div class="control">
    <input class="input" type="text" placeholder="Search" v-model="searchterm">
    {{findMatches(searchterm)}}
  </div>
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
    }
  }
};
</script>

<style>
.field {
  /* width: 100%; */
}
</style>

