<script setup>
const props = defineProps({
  transactions: Array
});

const emit = defineEmits(['transactionRemoved']);

const removeTransaction = (id) => {
  emit('transactionRemoved', id);
};
</script>

<template>
  <section v-show="transactions.length > 0" class="grid gap-y-5">
    <h3 class="text-3xl font-bold break-word">History</h3>
    <ul class="grid gap-y-3">
      <li 
        v-for="transaction in transactions" 
        :key="transaction.id"
        class="relative flex justify-between p-3 text-gray-700 bg-white shadow-lg border-r-4 group"
        :class="transaction.amount < 0 ? 'border-r-rose-600' : 'border-r-green-600'">
        {{ transaction.name }}
        <span>${{ transaction.amount }}</span>
        <button
          @click="removeTransaction(transaction.id)"
          class="absolute top-1/2 left-0 h-full px-4 text-xl font-bold text-white bg-red-600 opacity-0 -translate-x-full -translate-y-1/2 ease-in-out duration-500 group-hover:opacity-100"
          >X
        </button>
      </li>
    </ul>
  </section>
</template>