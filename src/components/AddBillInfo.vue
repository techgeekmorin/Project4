<script setup>
    import {ref, defineEmits} from 'vue';
    const text = ref('')
    const partyAmount = ref('')
    const billAmount = ref('')
    const tipPercent = ref('')

    const emit = defineEmits([
        'billSubmitted'
    ])

    const onSubmit = () =>{
        const billData ={
            text: text.value,
            partyAmount: parseInt(partyAmount.value),
            billAmount: parseFloat(billAmount.value).toFixed(2),
            tipPercent: parseFloat(tipPercent.value).toFixed(2),
            tipAmount: parseFloat((parseFloat(billAmount.value)*(parseFloat(tipPercent.value)/100))/parseInt(partyAmount.value)).toFixed(2)
        }

        emit('billSubmitted', billData)

        text.value = ''
        partyAmount.value = ''
        billAmount.value = ''
        tipPercent.value = ''
    }
</script>

<template>
    <h2>Add a New Bill</h2>
    <form id="form" @submit.prevent="onSubmit">
        <div class="form-control">
            <label for="text">Enter Event: </label>
            <input type="text" id="text" v-model="text" placeholder="Enter Event...">
        </div>
        <div class="form-control">
            <label for="partyAmount">Enter Party Amount: </label>
            <input type="text" id="partyAmount" v-model="partyAmount" placeholder="# of People in the Party">
        </div>
        <div class="form-control">
            <label for="billAmount">Enter Bill Amount: </label>
            <input type="text" id="billAmount" v-model="billAmount" placeholder="Enter Bill Total Here">
        </div>
        <div class="form-control">
            <label for="tipPercent">Enter Tip Percentage: </label>
            <input type="text" id="tipPercent" v-model="tipPercent" placeholder="Enter Tip % Here">
        </div>
        <button class="btn">Add Bill</button>

    </form>

</template>