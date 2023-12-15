<template>
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
  margin:1rem
}

 *{
   margin: 0;
   padding: 0;
 }

 img{
  max-width: 100%;
 }
</style>
