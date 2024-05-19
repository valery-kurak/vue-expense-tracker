<script setup>
import { ref } from 'vue';
import { useToast } from 'vue-toastification';

const name = ref('');
const amount = ref('');

const emit = defineEmits(['transactionSubmitted']); 

const toast = useToast();

const onSubmit = () => {
  if(!name.value || !amount.value) {
    toast.error('All fields must be filled.');
    return;
  };

  const transactionData = {
    name: name.value,
    amount: parseFloat(amount.value)
  };

  emit('transactionSubmitted', transactionData);

  name.value = '';
  amount.value = '';
};
</script>

<template>
  <section class="grid gap-y-5">
    <h3 class="text-3xl font-bold break-word">Add new transaction</h3>
    <form class="grid gap-y-5" @submit.prevent="onSubmit">
      <div class="grid gap-y-3">
        <label for="name" class="break-word">Name</label>
        <input type="text" id="name" v-model="name" class="p-3 border border-gray-400 rounded-sm outline-none cursor-pointer" placeholder="Enter name..." />
      </div>
      <div class="grid gap-y-3">
        <label for="amount" class="break-word">
          Amount <br />
          (positive - income, negative - expense)</label>
        <input type="text" id="amount" v-model="amount" class="p-3 border border-gray-400 rounded-sm outline-none cursor-pointer" placeholder="Enter amount..." />
      </div>
      <button class="p-3 text-white font-bold bg-violet-600 shadow-lg break-word ease-in-out duration-200 hover:bg-violet-500">Add transaction</button>
    </form>
  </section>
</template>