<template>
  <div class="blog-card-wrap">
    <H1 style="padding: 10px 100px" >Alumnos</H1>
    <br>
    <div class=" container">
     <table class="table table-dark table-hover">
        <thead>
            <tr>
                <th scope="col">Nombre</th>
                <th scope="col">Apellido</th>
                <th scope="col">Avances</th>
                <th scope="col">Email</th>
                <th scope="col">Privilegios</th>
                <th scope="col">Eliminar</th>
            </tr>
        </thead> 
        <tbody>
            <tr v-for="item in usuarios" :key="item.id">
                <th>{{item.firstName}}</th>
                <td>{{item.lastName}}</td>    
                <td v-if="profileAdmin">
                <router-link class=" ml-2 btn btn-primary"
                           :to="{
                            name: 'Avances',
                             params:{
                            alumnoid: item.id
                          }
                          }"
                          >
                          Editar
               </router-link>
               </td>
             <td>{{item.email}}</td> 
             <td>
                        <button class="btn btn-success" @click="Privilegios({id: item.id})" v-if="!item.privilegios"> Privilegios </button>
                        <button class="btn btn-warning" @click="SacarPrivilegios({id: item.id})" v-else> Sacar Privilegios </button>
                        
                </td> 
              <td>
                 <button class="btn btn-danger" @click="deleteHorario(item.id)"> Eliminar </button>
              </td>
            </tr>
        </tbody>
    </table>
     
    </div>
    
      <div class="small">
    <line-chart :chart-data="datacollection"></line-chart>
    <button @click="fillData()">Randomize</button>
  </div>


  </div>
</template>


<script>

import {mapState, mapActions} from 'vuex'
import LineChart from './LineChart.js'

export default {
    components: {
      LineChart
    },
    data () {
      return {
        datacollection: null
      }
    },
    mounted () {
      this.fillData()
    },
    created(){
     this.getUser()
    // this.verPrivilegios()
    },
    computed:{
     ...mapState(['usuarios']), 
    profileAdmin() {
      return this.$store.state.profileAdmin;   
         }
    },
     
    methods:{
      ...mapActions(['getUser','Privilegios','SacarPrivilegios']),
      fillData () {
        this.datacollection = {
          labels: [this.getRandomInt(), this.getRandomInt()],
          datasets: [
            {
              label: 'Data One',
              backgroundColor: '#f87979',
              data: [this.getRandomInt(), this.getRandomInt()]
            }, {
              label: 'Data One',
              backgroundColor: '#f87979',
              data: [this.getRandomInt(), this.getRandomInt()]
            }
          ]
        }
    },
     getRandomInt () {
        return Math.floor(Math.random() * (50 - 5 + 1)) + 5
      }
    }
  
}
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
