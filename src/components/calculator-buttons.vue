<template>
    <div>
        <button v-on:click="()=>action(character,classification)">{{ character }}</button>
    </div>
</template>

<script>
 export default {
    props:{
        character : String,
        action: Function,
        classification : String
    }
 }
</script>

<style>
.calculator-container button { 
    width: 50px; /* Adjust width as needed */
    height: 50px;  /* Adjust height as needed */
    margin: 5px; 
    border: 1px solid #ccc;
    background-color: #f0f0f0;
    font-size: 18px; 
    font-weight: bold;
    cursor: pointer;
 }
</style>