<template>
  <div class="add container">
    <h1 class="page-header">add costumer</h1>
    <form v-on:submit="addCustomer">
        <div class="well">
            <h4>Customer Info</h4>
            <div class="form-group">
                <label for="">First Name</label>
                <input type="text" class="form-control" placeholder="First" v-model="customer.first_name">
            </div>
            <div class="form-group">
                <label for="">Last Name</label>
                <input type="text" class="form-control" placeholder="Last" v-model="customer.last_name">
            </div>
        </div>
        <div class="well">
            <h4>Customer Contact</h4>
            <div class="form-group">
                <label for="">Email</label>
                <input type="text" class="form-control" placeholder="email@email.com" v-model="customer.email">
            </div>
            <div class="form-group">
                <label for="">Phone</label>
                <input type="text" class="form-control" placeholder="11111" v-model="customer.phone">
            </div>
        </div>
        <div class="well">
            <h4>Customer Location</h4>
            <div class="form-group">
                <label for="">Address</label>
                <input type="text" class="form-control" v-model="customer.address">
            </div>
        </div>
        <button type="submit" class="btn btn-primary">Submit</button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'add',
  data () {
    return {
      costumer: {}
    }
  },
  methods: {
      addCustomer(e){
          if(!this.customer.first_name || !this.customer.last_name || !this.customer.email){
              console.log('pleaseee render this');
          }else{
            let newCustomer = {
                first_name: this.customer.first_name,
                last_name: this.customer.last_name,
                email: this.customer.email,
                phone: this.customer.phone,
                address: this.customer.address
            }
            this.$http.post('http://slimapp/api/customer/add', newCustomer)
              .then(function(response){
                  this.$router.push({path: '/', query: {alert: 'Customer added!'}});
              });
            e.preventDefault();
          }
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
