<template>     
 <div>
  <div v-if="user" class="container-fluid" style="background: #eee"> 
    <div v-if="!user">
    <CarrouselInicio/>
      <br>
     <Footer3/>
    </div>
    <BlogPost v-if="!user" :post="welcomeScreen" />
    <BlogPost :post="post" v-for="(post, index) in blogPostsFeed" :key="index" />
    <div class="blog-card-wrap">
      <div class="container-fluid" style="background: #eee"> 
        <h3>Noticias recientes</h3>
        <div class="blog-cards">
          <BlogCard :post="post" v-for="(post, index) in blogPostsCards" :key="index" />
        </div>
      </div>
    </div>
  </div>
  
  
   <div v-if="!user" class="home">  
     <CarrouselInicio/>
      <br>
     <Footer3/>
      <br>
   </div>
  </div>
</template>



<script>

import CarrouselInicio from "../components/CarrouselInicio.vue"
import Footer3 from "../components/Footer3.vue"
import BlogPost from "../components/BlogPost.vue";
import BlogCard from "../components/BlogCard";

export default {
  name: "Home",
  components: {  Footer3, CarrouselInicio, BlogPost, BlogCard},
  data() {
    return {
       welcomeScreen: {
        title: "Hola!",
        blogPost:
          "Weekly blog articles with all things programming including HTML, CSS, JavaScript and more. Register today to never miss a post!",
        welcomeScreen: true,
        photo: "coding",
      },
    };
  },
  async created(){
     try {
       await this.$store.dispatch("getMostrar");
      } catch (error) {
       console.error(error);
      }
     try {
      await this.$store.dispatch("getHorarioSemana");
     } catch (error) {
      console.error(error);
     }
      await this.$store.dispatch("getPrivilegios", this.profileId);
      console.log("privilegios Home :", this.privilegios);
  },
  computed: {
    profileId() {
      return this.$store.state.profileId;
    },
   profileAdmin() {
      return this.$store.state.profileAdmin;   
       },
    privilegios() {
      return this.$store.state.privilegios;
    },
    blogPostsFeed() {
      return this.$store.getters.blogPostsFeed;
    },
    blogPostsCards() {
      return this.$store.getters.blogPostsCards;
    },
    user() {
      return this.$store.state.user;
    },
  }
};
</script>

<style lang="scss" scoped>


.home{ 
    background-color: #000000; 
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
