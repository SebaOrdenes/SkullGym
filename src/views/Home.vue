<template>
  <div class="home">
   
      <CarrouselInicio/>
      
   <!-- <BlogPost v-if="!user" :post="welcomeScreen" /> -->
     
      <div >
        <h2>Tu cambio comienza hoy, únete a skull fitness gym</h2>
        <router-link class="router-button" :to="{ name: 'Register'}"> Registrate ahora <Arrow class="arrow arrow-light" /> </router-link>
      </div>
  </div>
</template>








<script>


import CarrouselInicio from "../components/CarrouselInicio.vue"


export default {
  name: "Home",
  components: {   CarrouselInicio },
  data() {
    return {
    
    };
  },

};
</script>

<style lang="scss" scoped>


div {
  background-image: url("https://image.freepik.com/free-photo/old-black-background-grunge-texture-dark-wallpaper-blackboard-chalkboard-room-wall_1258-28313.jpg");
    color: white;
    padding: 100px 25px;
    width: 100%;
    font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
    display: flex;
    flex-direction: column;
    align-items: center;
  
}


.blog-card-wrap {
  h3 {
    font-weight: 300;
    font-size: 28px;
    margin-bottom: 32px;
  }
}
.updates {
  .container {
 

    padding: 100px 25px;
    display: flex;
    flex-direction: column;
    align-items: center;
    @media (min-width: 800px) {
      padding: 125px 25px;
      flex-direction: row;
    }
    .router-button {
      display: flex;
      font-size: 14px;
      text-decoration: none;
      @media (min-width: 800px) {
        margin-left: auto;
      }
    }
    h2 {
 
      font-weight: 300;
      font-size: 32px;
      max-width: 425px;
      width: 100%;
      text-align: center;
      text-transform: uppercase;
      @media (min-width: 800px) {
        text-align: initial;
        font-size: 40px;
      }
    }
  }
}
</style>