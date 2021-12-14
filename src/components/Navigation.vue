<template>
 
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Awesome CSS Responsive Navigation menus  </title>
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css">
  
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <header>
        <input type ="checkbox" name ="" id ="chk1">
        
           <div class="logo">    <router-link class="link" :to="{ name: 'Home' }"> <img src='../assets/skull_icon.png'></router-link>Skull Fitness Gym<router-link class="link" :to="{ name: 'Home' }"> <img src='../assets/skull_icon.png'></router-link> </div>
          
            <ul>
      <div class="nav-links">
        <ul v-show="!mobile">
            <li>
          <router-link class="link" :to="{ name: 'Home' }">Inicio</router-link>
          <router-link class="link" :to="{ name: 'Blogs' }">Blogs</router-link>
          <router-link v-if="admin" class="link" :to="{ name: 'CreatePost' }">Crear Post</router-link>
           <router-link v-if="admin" class="link" :to="{ name: 'CreateHorario' }">Crear Horario</router-link>
           
          <router-link v-if="!user" class="link" :to="{ name: 'Login' }">Login/Registro</router-link>
          <router-link v-if="user" class="link" :to="{ name: 'Horarios' }">Horarios</router-link>

          <router-link v-if="admin" class="link" :to="{ name: 'Alumnos' }">Alumnos</router-link>
          <router-link v-if="admin" class="link" :to="{ name: 'HistorialHorarios' }">Historial</router-link>
 
          <router-link v-if="user" class="link"
                           :to="{
                            name: 'Avances',
                             params:{
                            alumnoid:  this.$store.state.profileId
                          }
                          }"
                          >
                          Avances
        
          </router-link>

           <div @click="signOut" class="option" v-if="admin">
                   <p1>Salir</p1>
          </div>
              
        </li>
        </ul>
 
      </div>
        <menuIcon @click="toggleMobileNav" class="menu-icon" v-show="mobile" />
    <transition name="mobile-nav">
      <ul class="mobile-nav" v-show="mobileNav">
          <li>
        <router-link class="link" :to="{ name: 'Home' }">Inicio</router-link>
        <router-link class="link" :to="{ name: 'Blogs' }">Blogs</router-link>
        <router-link v-if="admin" class="link" :to="{ name: 'CreatePost' }">Crear Post</router-link>
         <router-link v-if="admin" class="link" :to="{ name: 'CreatePost' }">Crear Horario</router-link>
         <router-link v-if="user" class="link" :to="{ name: 'Horarios' }">Horarios</router-link>
        <router-link v-if="!user" class="link" :to="{ name: 'Login' }">Login/Register</router-link>
          </li>
      </ul>
    </transition>
                
            </ul>
            <div class="menu">
                <label for="chk1">
                    <i class="fa fa-bars"></i>
                </label>
            </div>
    </header>
  
</body>
</html>
</template>

<script>
import menuIcon from "../assets/Icons/bars-regular.svg";

import firebase from "firebase/app";
import "firebase/auth";

export default {
  name: "navigation",
  components: {
    menuIcon,
   
  },
  data() {
    return {
      profileMenu: null,
      mobile: null,
      mobileNav: null,
      windownWidth: null,
    };
  },
  created() {
    window.addEventListener("resize", this.checkScreen);
    this.checkScreen();
  },
  methods: {
    checkScreen() {
      this.windownWidth = window.innerWidth;
      if (this.windownWidth <= 750) {
        this.mobile = true;
        return;
      }
      this.mobile = false;
      this.mobileNav = false;
      return;
    },

    toggleMobileNav() {
      this.mobileNav = !this.mobileNav;
    },

    toggleProfileMenu(e) {
      if (e.target === this.$refs.profile) {
        this.profileMenu = !this.profileMenu;
      }
    },

    signOut() {
      firebase.auth().signOut();
      window.location.reload();
    },
  },
  computed: {
    user() {
      return this.$store.state.user;
    },
    admin() {
      return this.$store.state.profileAdmin;
    },
  },
};
</script>


<style scoped>

*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 	Courier New;
 
}
p1{
      text-decoration: none;
    color:#fff;
    font-weight: 600;
    text-transform: uppercase;
    padding: 10px 15px;
}
body{
    background: url('/assets/background1.png');
    background-size: cover;
    height: 0vh;
    background-position: center;
    
}
header{
    width:100%;
    height: 100px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    position: fixed;
    z-index: 99;
    box-shadow: 0 0 10px #000;
    background: rgba(0,0,0,0.5);



    

}
#chk1{
    display: none;
     
     
}
i{
    color: #fff;
    cursor: pointer;
}
header .logo{
    flex: 1;
    color:#fff;
     font-family: 	Courier New;
    margin-left: 50px;
    text-transform: uppercase;
    font-size: 30px;
}


header ul {
    flex:2;
    display: flex;
    justify-content: space-evenly;
}
header ul li{
    list-style: none;
}
header ul li a{
    text-decoration: none;
    color:#fff;
    font-weight: 600;
    text-transform: uppercase;
    padding: 10px 15px;
}
header ul li a:hover{
    border-bottom: 2px solid cadetblue;
}
header .menu{
    font-size: 2.5em;
    display: none;
}
@media(max-width:1000px){
    .search-box button{
        position: absolute;
    }
    header ul{
        position: fixed;
        top:100px;
        right: -100%;
        background: rgba(0,0,0,0.5);
        height: calc(100vh - 100px);
        width:50%;
        flex-direction: column;
        align-items: center;
        transition: right 0.5s linear;
    }
     
    header .menu{
        display: block;
        width:100px;
        text-align: center;
        
    }
    #chk1:checked ~ ul{
        right: 0;
        
    }
  
}
@media(max-width:600px){
    header .logo{
        font-size:10px;
        margin-left:8px;
    }
    header ul{
        width:100%;
    }
}


</style>
