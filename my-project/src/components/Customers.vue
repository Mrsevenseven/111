<template>
  <div class="customers container">
  	<Alert v-if="alert" v-bind:message="alert"></Alert>
    <h1 class="page-header">用户管理系统</h1>
  <table class="table table-striped">
    <thead>
      <tr>
        <th>name</th>
        <th>phone</th>
        <th>email</th>
        <th></th>
      </tr>
    </thead>
<tbody>
  <tr v-for="customer in customers">
    <td>{{customer.name}}</td>
    <td>{{customer.phone}}</td>
    <td>{{customer.email}}</td>
    <td><router-link class="btn btn-default" v-bind:to="'/customer/' + customer.id">详情</router-link></td>
  </tr>
</tbody>
</table>

  </div>
</template>

<script>
import Alert from './Alert'
export default {
  name: 'customers',
  data() {
    return {
      customers:[],
      alert:""
    }
  },

  methods: {
    fetchCustomers(){
      this.$http.get("http://localhost:3000/users")
      .then(function(response){
        // console.log(response)
        this.customers = response.body
      })
    }
  },
  created() {
    this.fetchCustomers()
  },
    components:{
  	Alert
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
