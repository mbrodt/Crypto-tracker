<template>
<div class="box boxtext"  @click="sendCoinEvent">
    <!-- <p>{{coin.name}}
      <br>
       {{coin.price_usd}}$
       <br>
        {{price_euro}}€
        </p> -->
        <h4>{{coin.name}}</h4>
        <div class="prices">
          <p>{{coin.price_usd | currencydecimal}}$</p>
          <p>{{price_euro | currencydecimal}}€</p>
        </div>

        <button class="my-button">More Info</button>

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
      return this.coin.price_usd * 0.83; //.toFixed(3);
    }
  },
  filters: {
    currencydecimal(value) {
      return parseFloat(value).toFixed(3);
    }
  }
};
</script>

<style>
.box {
  /* background: #c3e8c3; */
  /* padding: 10px; */
  /* background-image: linear-gradient(135deg, #43cbff 10%, #9708cc 100%); */
  border: 1px solid #000000;
  border-radius: 10px;
}
/* .box:hover {
  transform: translateY(-3px);
  box-shadow: 3px 3px #b8b8b8;
} */
.boxtext {
  color: #444444;
  text-align: center;
  font-size: 30px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-around;
}

.boxtext span {
  color: #666666;
}

h4 {
  font-weight: bold;
  color: #444444;
}

.prices {
  margin: 1rem;
}

.my-button {
  display: block;
  font-size: 1rem;
  background: #e76c67;
  border: 1px solid #e76c67;
  padding: 0.75rem 1rem;
  color: white;
  text-decoration: none;
  font-weight: 700;
  text-align: center;
}

.my-button:hover,
.my-button:focus {
  transform: translateY(-1px);
  background: #b95652;
  border: 1px solid #b95652;
}
</style>
