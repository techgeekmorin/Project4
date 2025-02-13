<script setup>
    import { defineProps, defineEmits} from 'vue';

    const props = defineProps({
        bills: {
            type: Array,
            require: true,
        }
    })

    const emit = defineEmits(['tipPaid'])

    const payTip = (id) => {
        emit('tipPaid', id)
    }

</script>

<template>
    <h2>Event History</h2>
    <ul id="list" class="list">
        <li v-for="x in bills" v-bind:key="x.id" v-bind:class="x.tipAmount">
            <div class="event-name"> {{ x.text }}</div> 
            <div class="bill-details">
            <p><span class="detail-title"> Bill Total:</span> ${{ x.billAmount }}</p> 
            <p><span class="detail-title">Number of People:</span> {{ x.partyAmount }}</p>
            <p><span class="detail-title"> Tip Percentage:</span> {{ x.tipPercent }}%</p>
            <p><span class="detail-title">Tip Amount:</span> ${{ x.tipAmount }}</p>
            <button @click="payTip(x.id)" class="delete-btn">Pay</button>
            </div>
        </li>


    </ul>
</template>