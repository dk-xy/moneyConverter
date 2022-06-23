<script setup>
import {
    ref,
    watchEffect
} from "vue";
import {
    inputValue
} from './../../state.js';

let euConvert = ref(0)
let usConvert = ref(0)
let btcConvert = ref(0)
let ethConvert = ref(0)
let isNotNull = ref(false);

// function round_float(x,num){
//   if(!parseInt(num))
//      num=0;
//   if(!parseFloat(x))
//     return false;
//   return Math.round(x*Math.pow(10,num))/Math.pow(10,num);
// }

fetch('https://cdn.jsdelivr.net/gh/fawazahmed0/currency-api@1/latest/currencies/eur.json')
    .then(resp => resp.json())
    .then(eurChangeRate => {

        const chfChangeRate = eurChangeRate.eur.chf
        const usChangeRate = eurChangeRate.eur.usd

        const btcChangeRate = eurChangeRate.eur.btc
        const ethChangeRate = eurChangeRate.eur.eth

        console.log(chfChangeRate)
        console.log(usChangeRate)

        watchEffect(() => {
            console.log(inputValue.value)
            if (inputValue.value > 0) {
                isNotNull.value = true;
                euConvert.value = (inputValue.value * chfChangeRate).toFixed(2)
                usConvert.value = (inputValue.value * usChangeRate).toFixed(2)

                btcConvert.value = (inputValue.value * btcChangeRate).toFixed(7)
                ethConvert.value = (inputValue.value * ethChangeRate).toFixed(7)

            } else {
                isNotNull.value = false;
            }

        })
    })
</script>

<template>
<div class="pageSection">Conversion d'euro</div>

<div class="convertResult" v-if="isNotNull">
    <div class="niceText"><b>{{inputValue}} EUR</b> équivaut à: </div>
        <div class="allRates">
        <div class="normalCurrency">
            <div class="rate">
                <div class="rateValue"><b>{{ euConvert }}</b></div>
                <div class="rateName">CHF</div>
            </div>
            <div class="rate">
                <div class="rateValue"><b>{{ usConvert }}</b></div>
                <div class="rateName">USD</div>
            </div>
        </div>
        <div class="cryptoCurrency">
            <div class="rate">
                <div class="rateValue"><b>{{ btcConvert }}</b></div>
                <div class="rateName">BTC</div>
            </div>

            <div class="rate">
                <div class="rateValue"><b>{{ ethConvert }}</b></div>
                <div class="rateName">ETH</div>
            </div>
        </div>
    </div>
    </div>

</template>
