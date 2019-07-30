<template>
  <q-page class="flex flex-center">
    <div>{{employeeData}}</div>

    <div class="row">

      <div class="col-sm-4">
        <p>Firstname</p>
        <button class="primary" @click="getFirstNameOnly()">Firstname</button>
        <div>
          <p>{{firstNameDataOnly}} </p>
        </div>
      </div>

      <div class="col-sm-4">
        <p>Lastname</p>
        <button class="primary" @click="getLastNameOnly()">Lastname</button>
        <div>
          <p>{{lastNameDataOnly}} </p>
        </div>
      </div>
 
     
        <button class="primary" @click="createNewEmployee()">Buat Baru</button>
  
       
    </div>

    
    <br>
    <br>
    <div class="row">
      <div class="col-sm-12"> 
              <v-md-date-range-picker></v-md-date-range-picker>
      </div>

    </div>



  </q-page>

</template>

<style>
</style>

<script>
import employee from "../api/employee/index";
import Vue from 'vue';
import VMdDateRangePicker from "v-md-date-range-picker";


export default {
  name: 'Employee',

  data(){
    return{
      employeeData:{},
      firstNameDataOnly:[],
      lastNameDataOnly:[],
      param:{
      "firstname": "Joko",
      "lastname": "string",
      "email": "JS@maka.com",
      "phone": "0898755425638826536498"
    }
  }
},

  methods:{
    getFirstNameOnly(){
      const self = this;
      employee.getEmployee(window).then(function(datas){
        console.log('ini data nama depan', datas)
        for(let i=0; i < datas.length; i++){ 
          self.firstNameDataOnly.push(datas[i].firstname)
        }
        return datas;
      }).catch(function(err){
        console.log(err)
      });
    },

    getLastNameOnly(){
      const self = this;
      employee.getEmployee(window).then(function(datas){
        console.log('ini data nama belakang', datas)
        for(let i=0; i < datas.length; i++){ 
          self.lastNameDataOnly.push(datas[i].lastname)
        }
        return datas;
      }).catch(function(err){
        console.log(err)
      });
    },

    createNewEmployee(){
       const self = this;
      employee.submitNewEmployee(window, self.param).then(function(result){
        return result;
      }).catch(function(err){
        console.log(err)
      });
    }

  },

  beforeCreate(){

      let self = this

      employee.getEmployee(window).then(function(datas){
          return datas
      }).then(function(res){
          console.log(res)
          self.employeeData = res
      }).catch(function(err){
          console.log(err)
      })

  }

}
Vue.use(VMdDateRangePicker);
</script>
