<script setup>
import chfComponent from './components/currencyConverters/chfComponent.vue';
import eurComponent from './components/currencyConverters/eurComponent.vue';
import usdComponent from './components/currencyConverters/usdComponent.vue';
import theNav from './components/theNav.vue';

import { page } from './state.js';
import { inputValue } from './state.js';



page.value = window.location.hash
console.log(page.value)
</script>

<template>
<div class="userSelection">
<div class="appHeader">
    <h1>Money Converter</h1>
    Welcome to Money ConverterChoose your currency bellow and see the different rates based on the price you input

</div>
<the-nav></the-nav>
<div>
</div>

<form @submit.prevent="convert" id="convertForm">
    <div class="formInput">
        <label for="inputValue">Valeur à convertir</label> <br>
        <input v-model="inputValue" placeholder="Valeur" type="number" id="convertFormValue" required>

    </div>
</form>
</div>
<div v-show="page==='#CHF'"><chfComponent></chfComponent></div>
<div v-show="page==='#EUR'"><eurComponent></eurComponent></div>
<div v-show="page==='#USD'"><usdComponent></usdComponent></div>


</template>

<style>

.allRates{
 width: 100%;
 margin: auto;
 display: flex;
 flex-direction: row;
 justify-content: center;
}

*{
  font-family: arial;
}

#app{
  width: 80%;
  margin: auto;
}

.userSelection{
  background-color: #fff3d4;
  padding: 20px 40px 20px 40px;
  border-radius: 20px;
}

.appHeader{
  width: 100%;
  margin: auto;
  text-align: center;
}

.rate {
    display: flex;
    flex-direction: row;
    justify-content: center;
    gap: 30px;
        margin: auto;
    margin-top: 20px;
    padding-bottom: 20px;
    border-bottom: solid 1px grey;
    width: 60%;

}

.convertResult{
    text-align: center;
}

#convertForm{
  text-align:center;
  margin: 40px 0px 40px 0px;
}

.pageSection{
  text-align: center;
  font-size: 18px;
  color: #787878;
  margin:40px 0px 40px 0px;
}

.niceText{
  margin: 0px 0px 40px 0px;
}


.normalCurrency{
  display: inline;

  margin: auto;
}

.cryptoCurrency{
  margin: auto;
}

.allRates{
  width: 50%;
  margin: auto;
}


</style>
