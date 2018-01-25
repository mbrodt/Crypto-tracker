<template>
<div class="box boxtext"  @click="sendCoinEvent">
    <slot></slot>
</div>
  
</template>

<script>
export default {
  data() {
    return {};
  },
  methods: {
    sendCoinEvent() {
      this.$root.$emit("coinclick");
    }
  }
};
</script>

<style>
.box {
  background: #c3e8c3;
  /* padding: 10px; */
  height: auto;
  border: 1px solid #000000;
  margin-bottom: 1em;
  border-radius: 20px;
}
.box:hover {
  transform: translateY(-5px);
  box-shadow: 3px 3px #b8b8b8;
}
.boxtext {
  color: red;
  text-align: center;
  font-size: 30px;
  /* max-width: 300px; */
}
</style>
