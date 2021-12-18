<template>
  <div>
     
     <p v-show="!this.mostrar" class="font-weight-bold">Mostrar a Todos a las: {{this.horaMostr}} {{this.horaMostrar}} {{this.most}} {{this.$store.state.mostrar}}</p>
     <p  v-show="mostrar"  class="font-weight-bold">Ingresa a que hora estará disponible para todos  {{this.most}} {{this.$store.state.mostrar}}</p>
     <b-form-timepicker v-show="mostrar" v-model="hora"  size="sm" ></b-form-timepicker>
     <button @click="HoraMostrar" v-if="mostrar"> Ingresar Hora a Mostrar </button>
     <button @click="HoraMostrar" v-else> Editar Hora a Mostrar </button>
                        
   
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
    beforeCreate() {
      console.log("beforeCreate")
    },
   async created(){
     try {
      await this.$store.dispatch("getMostrar");
     } catch (error) {
      console.error(error);
     }
      console.log("mostrar created:",this.mostrar)
      console.log("hora mostrar created",this.horaMostrar)
      
    },
   mounted() {
       this.$nextTick(function () {
       console.log("mounted")
       
    })
   },

    beforeUpdate() {
      console.log("beforeUpdate")
      this.most=this.mostrar
      console.log("mostrar beforeUpdate",this.most)
    },
    methods: {
    ...mapActions(['putMostrar']),
    HoraMostrar() {
     console.log("mostrar1:",this.mostrar)
     this.putMostrar({mostrar: !this.mostrar, hora: this.hora});
     //this.mostrar=!this.mostrar
     console.log("mostrar2:",this.mostrar)
     console.log(this.hora)
     this.horaMostr=this.hora
     this.most=!this.most
    },
  },
   computed: {
    //mostrar2() {
    //  console.log("mostrar state: computed")
    //  return this.$store.state.mostrar;
    //},
    mostrar() {
      console.log("mostrar getter: computed")
      return this.$store.getters.mostrar;
    },
     horaMostrar() {
      console.log("hora getter: computed")
      return this.$store.getters.horaMostrar;
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
