<script setup>
import {
    ref,
    watchEffect
} from "vue";
import {
    inputValue
} from './../../state.js';

let euConvert = ref(0)
let chfConvert = ref(0)
let btcConvert = ref(0)
let ethConvert = ref(0)
let isNotNull = ref(false);

fetch('https://cdn.jsdelivr.net/gh/fawazahmed0/currency-api@1/latest/currencies/usd.json')
    .then(resp => resp.json())
    .then(usdChangeRate => {
        const euChangeRate = usdChangeRate.usd.eur
        const chfChangeRate = usdChangeRate.usd.chf

        const btcChangeRate = usdChangeRate.usd.btc
        const ethChangeRate = usdChangeRate.usd.eth
        console.log(inputValue.value)
        watchEffect(() => {
            console.log(inputValue.value)
            if (inputValue.value > 0) {
                isNotNull.value = true;
                euConvert.value = (inputValue.value * euChangeRate).toFixed(2)
                chfConvert.value = (inputValue.value * chfChangeRate).toFixed(2)

                btcConvert.value = (inputValue.value * btcChangeRate).toFixed(7)
                ethConvert.value = (inputValue.value * ethChangeRate).toFixed(7)
            } else {
                isNotNull.value = false;
            }

        })
    })
</script>

<template>
    <div class="pageSection">Conversion de dollars américains</div>
    <div class="convertResult" v-if="isNotNull">
        <div class="niceText"><b>{{ inputValue }} USD</b> équivaut à: </div>
        <div class="allRates">
            <div class="normalCurrency">
                <div class="rate">
                    <div class="rateValue"><b>{{ euConvert }}</b></div>
                    <div class="rateName">EUR</div>
                </div>
                <div class="rate">
                    <div class="rateValue"><b>{{ chfConvert }}</b></div>
                    <div class="rateName">CHF</div>
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
