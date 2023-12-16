<template>
 <div class="hotelsContainer">
  <div class="header fade-in-down-header">
    <HeaderCom />
  </div>
    <ul  class="fade-in-down">
      <li v-for="hotel in hotels" :key="hotel.id" >
        <div class="cardCont">
          <div class="imgCont">
            <div class="imgOverlay">
              <h2 class="name">{{ hotel.name }}</h2>

              <div class="imgHolder" :style="{ backgroundImage: `url(${hotel.img})` }">  </div>
            </div>
            <div class="info">
              <div class="address">

                <p>{{ hotel.address }}</p>
                <p><RatingCom :rating="hotel.rating" /> </p>
              </div>
              <button class="booking" @click="bookHotel(hotel.id)">Book</button>
            </div>
          </div>
        </div>
      </li>
    </ul>

    <FooterCom />

    <div v-if="showBookingForm" class="formCont">
      <div class="form">
        <h3>Create Reservation</h3>
       <form @submit.prevent="submitBooking">
        <div class="inputWrapper">
          
          <label for="name">Name:</label>
          <input type="text" id="name" v-model="bookingForm.name" required />
        </div>
        
        
        <div class="inputWrapper">

          <label for="email">Email:</label>
          <input type="email" id="email" v-model="bookingForm.email" required />
         </div>
         <div class="inputWrapper">
 
        
         <label for="phone">Phone:</label>
        <input type="tel" id="phone" v-model="bookingForm.phone" required />
        </div> 
        <button type="submit" class="submit">Submit</button>
      </form>
      </div>
    </div >

  <div v-if="bookingSuccess">
    <h2>Thank you for booking with us!</h2>
  </div>
 </div >
</template >

  <script>


  import img1 from '../assets/1.jpg';  
  import img2 from '../assets/2.jpg';  
  import img3 from '../assets/3.jpg';  
  import img4 from '../assets/4.jpg';  
  import img5 from '../assets/5.jpg';  
  import img6 from '../assets/6.jpg';  


  import RatingCom from '../components/RatingCom.vue'
  import HeaderCom from '../components/HeaderCom.vue'
  import FooterCom from '../components/FooterCom.vue'
  import {ref, reactive} from "vue";

  export default {
    name: 'App',
    components: {
      RatingCom,
      HeaderCom,
      FooterCom
     },
    setup() {
      
    const hotels = ref([
    { id: 1, name: "Hotel A", address: "123 Main St", rating: 4, img:img1 },
    {id: 2, name: "Hotel B", address: "456 Oak St", rating: 3 , img: img2 },
    {id: 3, name: "Hotel C", address: "789 Pine St", rating: 5 , img: img3 },
    {id: 4, name: "Hotel D", address: "101 Elm St", rating: 2 , img: img4 },
    {id: 5, name: "Hotel E", address: "202 Maple St", rating: 3 , img: img5 },
    {id: 6, name: "Hotel F", address: "303 Birch St", rating: 5 , img: img6 },
    ]);

    const reserved = ref([]);
    const showBookingForm = ref(false);
    const bookingForm = reactive({
      id:"",
      name: "",
      email: "",
      phone: "",
    });

    const bookingSuccess = ref(false);

    function bookHotel(id) {
      // Retrieve hotel details based on the id
      const hotel = hotels.value.find((h) => h.id === id);

    // Show the booking form and set the hotel details
    showBookingForm.value = true;
    bookingForm.id = hotel.id;
    bookingForm.name = "";
    bookingForm.email = "";
    bookingForm.phone = "";
    }

    function submitBooking() {
      // Simulate booking submission and reset the form
      bookingSuccess.value = true;
      showBookingForm.value = false;

      reserved.value = [...reserved.value, bookingForm.id];
      setTimeout(() => {
          bookingSuccess.value = false;
      }, 3000);

    bookingForm.name = "";
    bookingForm.email = "";
    bookingForm.phone = "";
    }

    return {
      hotels,
      showBookingForm,
      bookingForm,
      bookingSuccess,
      bookHotel,
      submitBooking,
 
    };
 },
};
</script>

<style>
.hotelsContainer ul li {
    width: 30%;
    margin: 1rem;
    min-width: 300px;
    max-width: 90%;
    color: #fff;
}

.hotelsContainer ul {
    display: flex;
    justify-content: center;
    align-items: center;
    list-style: none;
    flex-wrap: wrap;
}
.imgCont {
    background-color: #292929;
    overflow: hidden;
    padding:1rem;
    border-radius: 0.7rem;
    border:1px solid #5a5a5a;
    box-shadow: 0 0 10px 0px #818181;
}
.imgOverlay{
  margin-bottom:1rem;
  border-radius: 0.7rem;
  overflow: hidden;
  position:relative
}

.imgOverlay .name{
    position:absolute;
}

.imgHolder {
  overflow: hidden;
  height: 300px;
  background-size: cover;
  background-position: center center;
  border-radius: 0.7rem;
}
.cardCont:hover .imgHolder{
  transform: scale(1.1);
  transition: 1s;
}


h2.name {
    position: absolute;
   z-index: 10;
    background: #08080880;
    right: 0;
    padding: 5px;
    top: 1.5rem;
    color: gold;
}

.info {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.booking{
padding: 10px 20px;
    border-radius: 0.7rem;
    /* font-weight: bold; */
    font-size: 1rem;
    cursor: pointer;
    border: 1px solid gold;
    background: #292929;
    color: gold;
    
}


.booking:hover{
    border: 1px solid #fff;
    color: #fff;
    box-shadow: 0 0 5px 1px white;

}

.fade-in-down-header {
  opacity: 0;
  transform: translateY(-50px);
  animation: fadeInDown 0.5s 0s ease-out forwards;
}
.fade-in-down {
  opacity: 0;
  transform: translateY(-50px);
  animation: fadeInDown 1s 0.5s ease-out forwards;
}
@keyframes fadeInDown {
  from {
    opacity: 0;
    transform: translateY(-50px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
 

/**************  form  *********** */

.formCont {
    position: fixed;
    top: 0;
    left: 0;
    height: 100vh;
    width: 100vw;
    background: #fafafa78;
    z-index: 30;
    display: flex;
    justify-content: center;
    align-items: center;
}

.submit {
    padding: 0.8rem 1rem;
    border-radius: 0.7rem;
    /* font-weight: bold; */
    font-size: 1.1rem;
    cursor: pointer;
    border: 1px solid gold;
    background: #292929;
    color: gold;
    margin-top: 1rem;
}

.form {
    background: black;
    padding: 2rem;
    border-radius: 10px;
    width: 400px;
    max-width: 90%;
}


.submit:hover{
    border: 1px solid #fff;
    color: #fff;
    box-shadow: 0 0 5px 1px white;

}


 
.inputWrapper input {
    width: 100%;
    padding: 10px;
    border-radius: 0.7rem;
    background: #292929;
    color: #fff;
}

.inputWrapper label {
    width: 100px;
    display: flex;
    /* font-weight: bold; */
    margin-bottom: 10px;
}
.inputWrapper {
    margin-bottom: 16px;
    width: 100%;
}


.form   h3 {
    font-size: 1.5rem;
    color: gold;
    border-bottom: 1px solid;
    padding: 15px 0;
    margin-bottom: 2rem;
}

 

</style>

 
 