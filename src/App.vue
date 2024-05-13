<template>
  <HeaderFile />
  <div class="conainer">
    <Balance :total="+total"/>
    <IncomeExpense :income="+income" :expense="+expense"/>
    <TransitionList :transactions="transactions" @deleteEmit="handleDelete"/> 
    <AddTransition @transitionSubmitted="handleSubmit"/>
  </div>

</template>

<script  setup>
import { ref, computed, onMounted } from 'vue';
import TransitionList from './components/TransitionList.vue';
import AddTransition from './components/AddTransition.vue';
import Balance from './components/Balance.vue';
import HeaderFile from './components/HeaderFile.vue';
import IncomeExpense from './components/IncomeExpense.vue';

const transactions = ref([])

onMounted(()=>{
  const savedTransitions = JSON.parse(localStorage.getItem('transitions'))
  if(savedTransitions){
    transactions.value = savedTransitions
  }
})

const saveToLocal = ()=>{
  localStorage.setItem('transitions',JSON.stringify(transactions.value))
}
//total sum
const total = computed(()=> {
  return transactions.value.reduce((acc,transaction)=>{
    return acc + transaction.amount
  },0)
})

// income
const income = computed(()=> {
  return transactions.value.filter((transaction)=>transaction.amount>0).reduce((acc,transaction)=>{
    return acc + transaction.amount;
  },0).toFixed(2);
})
// expenses
const expense = computed(()=> {
  return transactions.value.filter((transaction)=>transaction.amount<0).reduce((acc,transaction)=>{
    return acc + transaction.amount;
  },0).toFixed(2);
})
// generate unique key
const generateUniqueId=()=>{
  return Math.floor(Math.random()*1000000)
}

//handle transition Submit event
const handleSubmit = (transactionData)=>{
  transactions.value.push({
    id: generateUniqueId(),
    text: transactionData.text,
    amount: transactionData.amount
  })

  saveToLocal()

  alert("Transition added")
}
const handleDelete = (id)=>{
  transactions.value = transactions.value.filter((transaction)=>{
    return transaction.id != id
  })
  saveToLocal()
  alert("transition deleted :: " + id)
}

</script>

<style>

</style>
