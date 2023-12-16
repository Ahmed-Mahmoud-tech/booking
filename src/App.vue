<template>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Barlow+Semi+Condensed:wght@600;800&display=swap" rel="stylesheet">


 <HotelsCom  />
</template>

<script>
import HotelsCom from './components/HotelsCom.vue'

export default {
  name: 'App',
  components: {
    HotelsCom
  }
}
</script>

<style>
body{
  background-color: #181818;
  color:white;
  font-family: Arial, Helvetica, sans-serif;
  margin:1rem;
  margin-bottom: 0;
}

 *{
   margin: 0;
   padding: 0;
       box-sizing: border-box;
font-family: 'Barlow Semi Condensed', sans-serif;
}

 img{
  max-width: 100%;
 }
</style>
