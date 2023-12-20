<template>
  <h3>Add new transaction</h3>
  <form @submit.prevent="onSubmit" id="form">
    <div class="form-control">
      <label for="text">Text</label>
      <input type="text" id="text" v-model="text" placeholder="Enter text...">
    </div>
    <div class="form-control">
      <label for="amount">Amount <br>(negative - expense, positive - income)</label>
      <input type="text" id="text" v-model="amount" placeholder="Enter text...">
    </div>
    <button class="btn" type="submit">Add transaction</button>
  </form>
</template>

<script setup>
import { ref } from 'vue';
import { useToast} from 'vue-toastification'

const toast = useToast()
const text = ref('')
const amount = ref('')
const emit = defineEmits(['transactionSubmitted'])
const onSubmit = () => {
  if( !text.value || !amount.value) {
    toast.error('Boath fields must be filled')
    return
  }

  const transactionData = {
    text: text.value,
    amount: parseFloat(amount.value)
  }

  emit('transactionSubmitted', transactionData)

  text.value = ''
  amount.value = ''
}
</script>