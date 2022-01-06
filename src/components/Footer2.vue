<template>
  <footer>
    <div class="container">
      <div class="left">
        <div class="col-2">
          
          <ul>
            <router-link class="link" :to="{ name: 'Home' }">Inicio</router-link>
            <router-link class="link" :to="{ name: 'Blogs' }">Noticias</router-link>
            <router-link v-if="admin" class="link" :to="{ name: 'CreatePost' }">Create Post</router-link>
            <router-link v-if="user" class="link" :to="{ name: 'Horarios' }">Horarios</router-link>
            <router-link v-if="!user" class="link" :to="{ name: 'Login' }">Ingresar / Registrarse</router-link>
          </ul>
        </div>
        
      </div>
      <div class="right">
         <p> © {{año}} Skull fitness Gym. All Rights Reserved</p>
      </div>
    </div>
  </footer>
</template>

<script>

export default {
  name: "footer-vue",
  
  computed: {
    user() {
      return this.$store.state.user;
    },
    admin() {
      return this.$store.state.profileAdmin;
    },
    año(){
       let date =  new Date().getFullYear();
       return date;
     }
  },
};
</script>

<style lang="scss" scoped>
footer {
  background-image: url("../assets/5.jpg");
  margin-top: auto;
  padding: 115px 150px;
  background-color: #303030;
  .container {
    .link{
      font-family: 'Courier New', Courier, monospace;
    }
    
    display: flex;
    flex-direction: column;
    gap: 32px;
    @media (min-width: 800px) {
      flex-direction: row;
      gap: 0px;
    }

    > div {
      display: flex;
      flex: 1;
    }

    .left {
      gap: 32px;
      color: #fff;
      display: flex;
      flex-direction: column;
      align-items: center;
      @media (min-width: 800px) {
        flex-direction: row;
        align-items: initial;
        gap: 0;
      }

      .header {
        font-family: 'Courier New', Courier, monospace;
        text-align: center;
        font-size: 30px;
        color: #fff;
        margin-bottom: 16px;
        text-decoration: none;
        font-weight: 550;
        @media (min-width: 800px) {
          text-align: initial;
        }
      }
      ul {
      
        gap: 5px;
        list-style: none;
        display: flex;
      }

      .col-1,
      .col-2 {
        font-family: 'Courier New', Courier, monospace;
        gap: 32px;
        display: flex;
        flex: 1;
        @media (min-width: 800px) {
          gap: 0;
        }
      }

      .col-1 {
        flex-direction: column;

        h2 {

          text-align: center;
          @media (min-width: 800px) {
            text-align: initial;
          }
        }
        ul {
          margin-top: auto;
      

          li {
            
            display: flex;
            align-items: center;
            .svg-icon {
              width: 24px;
              height: auto;
              color: #fff;
            }
          }
        }
      }

      .col-2 {
        ul {
          height: 100%;
          justify-content: center;
          flex-direction: row;
          flex-wrap: wrap;
          @media (min-width: 800px) {
            flex-direction: column;
          }
          .link {
            font-size: 16px;
            font-weight: 500;
            color: #fff;
            text-decoration: none;
          }
        }
      }
    }

    .right {
      gap: 32px;
      color: #fff;
      align-items: center;
      flex-direction: column;
      @media (min-width: 800px) {
        align-items: flex-end;
        gap: 0;
      }
    }

    p {
      margin-top: auto;
      max-width: 40%;
    }
  }
}
</style>

