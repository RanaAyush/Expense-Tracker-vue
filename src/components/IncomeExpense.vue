<template>
    <div class="inc-exp">
        <div>
            <h4>Income</h4>
            <p id="money-plus" class="moneyp">$+{{income}}</p>
        </div>
        <div>
            <h4>Expense</h4>
            <p id="money-minus" class="moneym">
                ${{expense}}
            </p>
        </div>
    </div>
</template>
<script setup>
import { defineProps } from "vue";


const props = defineProps({
  income: {
    type: Number,
    required: true,
  },
  expense:{
    type:Number,
    required: true,
  }
});
</script>
<style>
.inc-exp{
    display: flex;
    justify-content: space-between;
    margin: 5px 0;
}
.inc-exp >div{
    flex: 1;
    text-align:  center;
    margin: 0 5px;
}

</style>