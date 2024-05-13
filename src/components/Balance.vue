<template>
    <h4>Your Balance</h4>
    <h1 id="balance" :class="total < 0 ? 'moneym':'moneyp'"> <span style="color:black">$</span>{{total}} </h1>
</template>
<script setup>
import { defineProps } from "vue";

const props = defineProps({
    total: {
        type: Number,
        required: true,
    },
})
</script>