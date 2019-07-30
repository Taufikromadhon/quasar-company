<template>
  <q-page class="flex flex-center">
     
    <div class="q-pa-md">
    <q-table
      title="Roles"
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
import roles from "../api/roles/index";



export default {
  name: 'Roles',

 data () {
    return {
      columns: [
        {
          name: 'roleName',
          required: true,
          label: 'Role Name',
          align: 'left',
          field: row => row.roleName,
          format: val => `${val}`,
          sortable: true
        },
        { 
          name: 'tanggalMasuk', 
          align: 'center', 
          label: 'Tanggal Masuk', 
          field: row => row.tanggalMasuk , 
          sortable: true 
        },
        { 
          name: 'statusRole', 
          label: 'Status Role', 
          field: row => row.statusRole , 
          sortable: true 
        },
        
        { 
          name: 'deskripsiRole', 
          label: 'Deskripsi Role', 
          field: row => row.deskripsiRole  
        },
        
      ],
      data: []
    }
  },

  beforeCreate(){

      let self = this

      roles.getAllRoles(window).then(function(datas){
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
