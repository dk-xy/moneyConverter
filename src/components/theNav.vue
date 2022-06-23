<script setup>
import { page } from '../state.js'



window.addEventListener('hashchange', () => {
    console.log(window.location.hash)
    page.value = window.location.hash

    


})


</script>

<template>
<nav>
    <ul class="navigation">
        <li>
            <a href="#CHF">CHF</a>
        </li>
        <li>
            <a href="#EUR">EUR</a>
        </li>
        <li>
            <a href="#USD">USD</a>
        </li>
    </ul>

</nav>
</template>

<style scoped>
nav{
    text-align: center;

    margin: auto;
}

ul {
  list-style-type: none;

  display: flex;
  flex-direction: row;
  gap: 10px;
  margin: auto;
  justify-content: center;
  margin-top:20px;
}

li{

    background-color: #ffa238;
        border-radius: 10px;
}

li:hover{
    transition: 1s;
     background-color: #000000;
}

li a:active{
     background-color: #000000;
}

li a:link, li a:visited {
    text-decoration: none;
    color: white;
    font-weight: 800;
}

li a{
    display: block;
    padding: 20px 40px 20px 40px;

}
</style>
