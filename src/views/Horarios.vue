<template>
  <div class="blog-card-wrap">
   <h3> Horarios disponibles: </h3>
    <div v-show="mostrarConPrivilegios" class="blog-cards container">
      <HorariosNoTomados />
    </div>
    <div v-show="mostrarConPrivilegios" class="blog-cards container">
      <HorariosTomados />
    
    </div>

    <div v-show="mostrarTodos" class="blog-cards container">
      <HorariosNoTomados />
    </div>
    <div v-show="mostrarTodos" class="blog-cards container">
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
      privilegio : null,
      mostrarTodos: null,
      mostrarConPrivilegios:null
    }
  },
  async created(){
     try {
       await this.$store.dispatch("getMostrar");
      } catch (error) {
       console.error(error);
      }
      let fecha1 = this.$store.getters.MostrarHorario;
      console.log("mostrar created:",fecha1)
      await this.$store.dispatch("getPrivilegios", this.profileId);
      console.log("privilegios... :", this.privilegios);
      this.mostrar=this.privilegios;
      if (fecha1==false && this.mostrar==true){
           console.log("Mostrar con Privilegios... :", this.privilegios);
           this.mostrarConPrivilegios=true;
      }else if(fecha1==false && this.mostrar==false){
          console.log("No muestra ya que no tiene privilegios ");
          this.mostrarTodos=false;
      }else if(fecha1==true){
          console.log("Mostrar a Todos" );
          this.mostrarTodos=true;
      }
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
    MostrarHorario() {
      return this.$store.getters.MostrarHorario;
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
