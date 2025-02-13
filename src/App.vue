<script setup>

  import Header from './components/Header.vue';
  import TipOwed from './components/TipOwed.vue';
  import AddBillInfo from './components/AddBillInfo.vue';
  import BillList from './components/BillList.vue';
  import {ref, computed, onMounted} from 'vue';
   
  const bills = ref([])

  const tipOwed = computed(()=>{
    return bills.value.reduce((acc, x)=>{
      return acc+parseFloat(x.tipAmount)
    },0)
  })
  
  const handleBill = (billData) => {
    bills.value.push({
      id: generateID(),
      text: billData.text,
      partyAmount: billData.partyAmount,
      billAmount: billData.billAmount,
      tipPercent: billData.tipPercent,
      tipAmount: (billData.tipAmount).toFixed(2),
    })
    saveToLocalStorage()
  }

  const generateID = () =>{
    return Math.floor(Math.random()*10000000)
  }

  const handlePaid = (id) =>{
    bills.value = bills.value.filter((x) => x.id !== id)
    saveToLocalStorage()
  }

  const saveToLocalStorage = () => {
    localStorage.setItem('bills', JSON.stringify(bills.value))
  }

    onMounted( () => {
      const savedbills = JSON.parse(localStorage.getItem('bills'))

      if(savedbills){
        bills.value = savedbills
      }
    })
</script>

<template>

  <Header></Header>
  <div class="container">
    <TipOwed :totalOwed="tipOwed"></TipOwed>
    <AddBillInfo @billSubmitted="handleBill"></AddBillInfo>
    <BillList :bills="bills" @tipPaid="handlePaid"></BillList>
  </div>

</template>