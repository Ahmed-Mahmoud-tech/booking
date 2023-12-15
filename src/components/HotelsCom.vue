<template>
 <div class="hotelsContainer">
 
    <ul>
      <li v-for="hotel in hotels" :key="hotel.id">
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
              <button class="booking" @click="bookHotel(hotel.id)">Reserve</button>
            </div>
          </div>
        </div>
      </li>
    </ul>

    <div v-if="showBookingForm" class="formCont">
      <h2>Booking Details</h2>
      <form @submit.prevent="submitBooking">
        <label for="name">Name:</label>
        <input type="text" id="name" v-model="bookingForm.name" required />
        <br />
        <label for="email">Email:</label>
        <input type="email" id="email" v-model="bookingForm.email" required />
        <br />
        <label for="phone">Phone:</label>
        <input type="tel" id="phone" v-model="bookingForm.phone" required />
        <br />
        <button type="submit">Submit</button>
      </form>
    </div >

  <div v-if="bookingSuccess">
    <h2>Thank you for booking with us!</h2>
  </div>
 </div >
</template >

  <script>


  import RatingCom from '../components/RatingCom.vue'
  import {ref, reactive} from "vue";

  export default {
    name: 'App',
    components: {
      RatingCom
     },
    setup() {
      
    const hotels = ref([
    { id: 1, name: "Hotel A", address: "123 Main St", rating: 4, img:"https://www.lovidhu.com/uploads/posts-seo/2021/05/polonnaruwa-vatadage-sri-lanka.jpg"},
    {id: 2, name: "Hotel B", address: "456 Oak St", rating: 3 , img:"https://classiclanka.com/wp-content/uploads/2022/06/Galle.webp"},
    {id: 3, name: "Hotel C", address: "789 Pine St", rating: 5 , img: "https://haleyblackall.com/wp-content/uploads/2020/12/things-to-do-in-Kandy-20.jpg" },
    {id: 4, name: "Hotel D", address: "101 Elm St", rating: 2 , img: "https://www.lovidhu.com/uploads/posts-seo/2021/05/polonnaruwa-vatadage-sri-lanka.jpg" },
    {id: 5, name: "Hotel E", address: "202 Maple St", rating: 3 , img: "https://www.jetwinghotels.com/jetwingviluyana/wp-content/uploads/sites/2/2017/09/dambulla-temple-1.jpg" },
    {id: 6, name: "Hotel F", address: "303 Birch St", rating: 5 , img: "https://media-cdn.tripadvisor.com/media/photo-s/16/db/91/41/the-city-now-a-world.jpg" },
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
    margin: 0.5rem;
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
  transform: scale(1.3);
  transition: 1s;
}


h2.name {
    position: absolute;
   z-index: 10;
    background: #08080880;
    right: 0;
    padding: 5px;
    top: 2rem;
    color: gold;
}

.info {
    display: flex;
    justify-content: space-between;
}

.booking{
padding: 0 20px;
    border-radius: 0.7rem;
    font-weight: bold;
    font-size: 1rem;
    cursor: pointer;
    border: 1px solid gold;
    background: #292929;
    color: gold;
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


</style>

 
 