<template>
  <q-page class="flex flex-center">
     
    <div class="q-pa-md">
    <q-table
      title="Projects"
      :data="data"
      :columns="columns"
      row-key="name"
      dark
      color="amber"
    />
  </div>

  </q-page>

</template>

<style>
</style>

<script>
import project from "../api/project/index";



export default {
  name: 'Project',

 data () {
    return {
      columns: [
        {
          name: 'projectName',
          required: true,
          label: 'Project Name',
          align: 'left',
          field: row => row.projectName,
          format: val => `${val}`,
          sortable: true
        },
        { 
          name: 'capasity', 
          align: 'center', 
          label: 'Capasity', 
          field: row => row.capasity , 
          sortable: true 
        },
        { 
          name: 'startDate', label: 'Start Date', 
          field: row => row.startDate , 
          sortable: true 
        },
        
        { 
          name: 'endDate', 
          label: 'End Date', 
          field: row => row.endDate  
        },
        
        { 
          name: 'status', 
          label: 'Status', 
          field: row => row.status  
        },
        
        { 
          name: 'createAt', 
          label: 'Create At', 
          field: row => row.createAt  
        
        },        
      ],
      data: []
    }
  },

  beforeCreate(){

      let self = this

      project.getAllProject(window).then(function(datas){
          return datas
      }).then(function(res){
          console.log(res)
          self.data = res
      }).catch(function(err){
          console.log(err)
      })

  },


}
</script>
