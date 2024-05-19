<script setup>
defineProps({
  total: Number
});
</script>

<template>
  <section class="break-word">     
    <h2 class="text-xl">YOUR BALANCE</h2>
    <h3 class="text-3xl font-bold">${{ total }}</h3>
  </section>
</template>