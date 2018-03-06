<template>
<div class="box boxtext"  @click="sendCoinEvent">
    <p>{{coin.name}}
      <br>
       {{coin.price_usd}}$
       <br>
        {{price_euro}}€
        </p>
</div>
  
</template>

<script>
export default {
  data() {
    return {};
  },
  props: ["coin"],
  methods: {
    sendCoinEvent() {
      this.$root.$emit("coinclick", this.coin);
    }
  },
  computed: {
    price_euro: function() {
      //todo pull in real conversion rate
      return (this.coin.price_usd * 0.83).toFixed(3);
    }
  }
};
</script>

<style>
.box {
  /* background: #c3e8c3; */
  /* padding: 10px; */
  background-image: linear-gradient(135deg, #43cbff 10%, #9708cc 100%);
  height: auto;
  border: 1px solid #000000;
  margin-bottom: 1em;
  border-radius: 10px;
}
.box:hover {
  transform: translateY(-3px);
  box-shadow: 3px 3px #b8b8b8;
}
.boxtext {
  color: #34323a;
  text-align: center;
  font-size: 30px;
  /* max-width: 300px; */
}
</style>
