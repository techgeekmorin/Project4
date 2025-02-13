<script setup>
    import {defineProps} from 'vue'

    const props = defineProps({
        totalOwed: {
            type: Number,
            require: true,
        }
    })
</script>

<template>
    <h2>Tip Amount Owed By You</h2>
    <h3 id="tipOwed">{{ totalOwed }}</h3>




</template>