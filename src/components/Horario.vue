<template>
  <div>

    
    <div class="container"> 
      <h4>Fecha</h4>
      <b-form-datepicker v-model="clase.fecha" size="sm" class="mb-3"></b-form-datepicker>

       <br>
      <h4>Hora</h4>
      <b-col md="auto">
      <b-time class="border rounded p-2 mb-3" v-model="clase.horas" locale="en" size="sm" ></b-time>
       </b-col>
      <br>

      <h4>Tipo de clase</h4>
      <b-form-group>
      <b-form-select v-model="clase.tipo" :options="optionsTipo" size="sm" class="mb-3"></b-form-select>
      </b-form-group>
  
      <br>
      <h4>Cupos</h4>
      <b-input-group class="mb-3">
       <b-input-group-prepend is-text>
        <b-icon icon="person-fill"></b-icon>
       </b-input-group-prepend>
      <b-form-input type="text" placeholder="Ingresa los cupos que estarán disponibles"
       v-model.trim="clase.cupos" ></b-form-input>
      </b-input-group>
    <br>
  
    <b-button variant="dark" type="submit" :disabled="bloquear">
      Procesar
    </b-button>

   </div>
  </div>
</template>

<script>
export default {
  props: {
    clase: Object,
  },
  computed: {
    bloquear() {
      return this.clase.cupos === '' ? true : false;
    },
  },
  data() {
    return {
      timepicker:'',
      fecha:null,
      semana:null,
      horas: null,
      tipo: null,
      cupos:null,
      optionsTipo: [
        { value: null, text: "Selecciona el tipo de clase" },
        { value: "Espalda", text: "Espalda" },
        { value: "Cardio", text: "Cardio" },
        { value: "Piernas", text: "Piernas" },
        { value: "Pecho", text: "Pecho" },
        { value: "A eleccion", text: "A elección" },
      ],
    };
  },
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
