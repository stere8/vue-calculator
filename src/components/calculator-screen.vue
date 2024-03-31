<template>
  <div class="screen-output">{{ displayValue }}</div> 
</template>

  <script>
  export default {
    props: ['data'], 
    computed: {
      formattedData() {
        let num = parseFloat(this.data); 
        if (!isNaN(num)) {
          return num.toLocaleString(); 
        } else {
          return this.data; // Return the original data on error
        }
      }
    }
  }
  </script>
  
  <style>
  .screen-output {
    background-color: #f0f0f0;
    border: 1px solid #ccc;
    padding: 15px; 
    font-size: 24px;
    font-family: 'Courier New', monospace; 
    text-align: right; 
    box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.1); 
    overflow: hidden; 
    white-space: nowrap; 
    text-overflow: ellipsis; 
  }
  </style>
  