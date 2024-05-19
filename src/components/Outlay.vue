<script setup>
const props = defineProps({
  income: Number,
  expense: Number
});
</script>

<template>
   <section class="grid grid-cols-2 py-4 text-xl text-center shadow-md bg-white">
    <div class="px-4 border-r border-slate-400 break-word">
      <h4>Income</h4>
      <p class="text-green-600">${{ income }}</p>
    </div>
    <div class="px-4 break-word">
      <h4>Expense</h4>
      <p class="text-rose-600">${{ expense }}</p>
    </div>
  </section>
</template>