<template>
  <div class="customers container">
  <Alert v-if="alert" v-bind:message="alert" />
    <h1 class="pager-header">Customers</h1>
    <table class="table table-striped">
      <thead>
        <tr>
          <th>First Name</th>
          <th>Last Name</th>
          <th>Email</th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="costumer in costumers">
          <td>{{costumer.first_name}}</td>
          <td>{{costumer.last_name}}</td>
          <td>{{costumer.email}}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import Alert from './Alert';
export default {
  name: 'customers',
  data () {
    return {
      customers: [],
      alert: '' 
    }
  },
  methods: {
    fetchCustomers(){
      this.$http.get('http://slimapp/api/customers')
        .then(function(response){
          console.log(response.body)
        });
    }
  },
  created: function(){
    if(this.$route.query.alert){
      this.alert = this.$route.query.alert;
    }
  },
  updated: function(){
    this.fetchCustomers();
  },
  components: {
    Alert
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only  min 38 -->
<style scoped>

</style>
