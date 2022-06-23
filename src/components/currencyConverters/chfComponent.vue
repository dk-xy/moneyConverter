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

fetch('https://cdn.jsdelivr.net/gh/fawazahmed0/currency-api@1/latest/currencies/chf.json')
    .then(resp => resp.json())
    .then(chfChangeRate => {
        console.log(chfChangeRate)
        console.log(chfChangeRate.chf.eur)
        const euChangeRate = chfChangeRate.chf.eur
        const usChangeRate = chfChangeRate.chf.usd

        const btcChangeRate = chfChangeRate.chf.btc
        const ethChangeRate = chfChangeRate.chf.eth
        console.log(euChangeRate)
        console.log(usChangeRate)
        console.log(inputValue.value)
        watchEffect(() => {
            console.log(inputValue.value)
            if (inputValue.value > 0) {
                isNotNull.value = true;
                euConvert.value = (inputValue.value * euChangeRate).toFixed(2)
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
  <div class="pageSection">Conversion de Francs Suisses</div>
    <div class="convertResult" v-if="isNotNull">
        <div class="niceText"><b>{{ inputValue }} CHF</b> équivaut à: </div>
        <div class="allRates">
            <div class="normalCurrency">
                <div class="rate">
                    <div class="rateValue"><b>{{ euConvert }}</b></div>
                    <div class="rateName">EUR</div>
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

<style scoped>

</style>
