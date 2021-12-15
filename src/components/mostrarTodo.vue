<template>
  <div>
     
     <p v-show="!mostrar" class="font-weight-bold">Mostrar a Todos a las: {{this.horaMostr}} {{this.horaMostrar}}</p>
     <p  v-show="mostrar"  class="font-weight-bold">Ingresa a que hora estará disponible para todos</p>
     <b-form-timepicker v-show="mostrar" v-model="hora"  size="sm" ></b-form-timepicker>
     <button @click="HoraMostrar"> Hora a Mostrar </button>

   
  </div>
</template>

<script>
import { mapActions} from 'vuex'
export default {
  
  data() {
    return {
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
    },
    methods: {
    ...mapActions(['putMostrar']),
    HoraMostrar() {
     var estado = this.mostrar;
     this.putMostrar({mostrar:!estado,hora: this.hora});
     console.log(this.mostrar)
     this.horaMostr=this.hora
    },
  },
   computed: {
    mostrar() {
      return this.$store.state.mostrar;
    },
     horaMostrar() {
      return this.$store.getters.horaMostrar;
    },
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
