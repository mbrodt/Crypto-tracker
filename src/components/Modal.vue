<template>
<div class="modal is-active">
  <div class="modal-background"></div>
  <div class="modal-card">
    <header class="modal-card-head">
      <p class="modal-card-title">Modal title</p>
      <button class="delete" aria-label="close" @click="$emit('close')"></button>
    </header>
    <section class="modal-card-body">
      <!-- Content ... -->
    </section>
  </div>
</div>
</template>

<script>
// import bulma from "../assets/css/bulma.css";

export default {};
</script>
