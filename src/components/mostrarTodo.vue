<template>
  <div>
     <br>
     <br>
     <p v-show="!this.mostrar" class="font-weight-bold">Mostrar a Todos en ---> {{this.horaMostrar}} {{this.$store.state.mostrar}} - {{this.$store.getters.MostrarHorario}}</p>
    <!--    <p  v-show="mostrar"  class="font-weight-bold">Ingresa a que hora estará disponible para todos  {{this.most}} {{this.$store.state.mostrar}}</p>
   <b-form-timepicker v-show="mostrar" v-model="hora"  size="sm" ></b-form-timepicker> -->
     <h4 v-show="mostrar">Ingresa en cuantas horas estará disponible para todos</h4>
     <input v-show="mostrar" v-model="hora" placeholder="Ingresar Horas">
     <p v-show="mostrar"> Estará disponible para todos en: {{this.hora}} {{this.$store.state.mostrar}}</p>
     <button @click="HoraMostrar" v-if="mostrar"> Ingresar Hora a Mostrar </button>
     <button @click="SacarHoraMostrar" v-else> Editar Hora a Mostrar </button>
                        
   
  </div>
</template>

<script>
import { mapState,mapActions} from 'vuex'
export default {
  
  data() {
    return {
      horaMostr:null,
      hora:null,
      most:null
    };
  },
   async created(){
     try {
      await this.$store.dispatch("getMostrar");
     } catch (error) {
      console.error(error);
     }
      //console.log("mostrar created:",this.mostrar)
      
      let fecha1 = this.$store.getters.horaMostrar;
      console.log("mostrar created:",fecha1)
      
    },
     
     
    methods: {
    ...mapActions(['putMostrar']),

    SacarHoraMostrar() {
     this.putMostrar({mostrar: !this.mostrar, hora: this.hora});
     this.most=!this.most 
    },
    HoraMostrar() {
     
     let hoy = new Date();
     let mañana = 1000 * 60 * 60 * this.hora;
     let diferencia = hoy.getTime() + mañana;
     let fechaenhoras= new Date(diferencia);
     this.putMostrar({mostrar: !this.mostrar, hora: fechaenhoras});
     console.log("fecha con horas: ",fechaenhoras);
     this.horaMostrar = this.fechaenhoras;
     //console.log(this.hora)
     this.most=!this.most
     //console.log("mostrar2:",this.most)
    },

  },
   computed: {
  
    mostrar() {
      return this.$store.getters.mostrar;
    },
     horaMostrar() {
      return this.$store.getters.horaMostrar;
    },
    MostrarHorario() {
      return this.$store.getters.MostrarHorario;
    },
    ...mapState(['mostrar']),
  }
};
</script>

<style lang="scss" scoped>
html,body{
            min-height: 10vh;
            min-width: 10vw;
        }
        .parent{
            height: 10vh;
        }
        .parent>.row{
            display: flex;
            align-items: center;
            height: 50%;
        }
        .col img{
            height:100px;
            width: 100%;
            cursor: pointer;
            transition: transform 1s;
            object-fit: cover;
        }
        .col label{
            overflow: hidden;
            position: relative;
        }
        .imgbgchk:checked + label>.tick_container{
            opacity: 1;
        }
/*         aNIMATION */
        .imgbgchk:checked + label>img{
            transform: scale(1.25);
            opacity: 0.3;
        }
        .tick_container {
            transition: .5s ease;
            opacity: 0;
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            -ms-transform: translate(-50%, -50%);
            cursor: pointer;
            text-align: center;
        }
        .tick {
            background-color: #808080;
            color: white;
            font-size: 16px;
            padding: 6px 12px;
            height: 40px;
            width: 40px;
            border-radius: 100%;
        }
div#form{
margin: auto;
padding: 60px 120px;
width: 10;
height: 10;
background-color:gray;
