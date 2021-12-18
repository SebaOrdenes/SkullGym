<template>
  <div class="blog-card-wrap">
   <h3 v-if="profileAdmin" > No mostrar antes de: </h3>
    <div v-show="mostrar" class="blog-cards container">
      <HorariosNoTomados />
    </div>
    <div v-show="mostrar" class="blog-cards container">
      <HorariosTomados />
    </div>
  </div>
</template>


<script>
import HorariosNoTomados from "../components/HorariosNoTomados";
import HorariosTomados from "../components/HorariosTomados";
//import firebase from "firebase/app";
//import "firebase/storage";
//import db from "../firebase/firebaseInit";
export default {
  name: "horarios",
  components: { HorariosTomados, HorariosNoTomados },
  data() {
    return {
      mostrar: true,
      privilegio : null
    }
  },
  async created(){
      await this.$store.dispatch("getPrivilegios", this.profileId);
      //console.log("privilegios... :", this.privilegios);
      //this.mostrar=this.privilegios;
    },
  methods: {
           
  //if timestamp sea mayor a x && privilegios === False
  // => mostrar ===True
  // else-if privilegios === True
  // => mostrar ===True
     
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
  }
};
</script>


<style lang="scss" scoped>
.blog-cards {
  position: relative;
  .toggle-edit {
    display: flex;
    align-items: center;
    position: absolute;
    top: -70px;
    right: 0;
    span {
      margin-right: 16px;
    }
    input[type="checkbox"] {
      position: relative;
      border: none;
      -webkit-appearance: none;
      background: #fff;
      outline: none;
      width: 80px;
      height: 30px;
      border-radius: 20px;
      box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
    }
    input[type="checkbox"]:before {
      content: "";
      position: absolute;
      width: 30px;
      height: 30px;
      border-radius: 20px;
      top: 0;
      left: 0;
      background: #303030;
      transform: scale(1.1);
      transition: 750ms ease all;
      box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
    }
    input:checked[type="checkbox"]:before {
      background: #fff;
      left: 52px;
    }
  }
}
</style>
