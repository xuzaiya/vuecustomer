<template>
    <div class="customers container">
      <alert v-if="alert" v-bind:message="alert"></alert>
      <h1 class="page-header">用户管理系统</h1>
      <input type="text" class="form-control" placeholder="搜索" v-model="filterInput">
      <table class="table table-striped">
        <thead>
          <tr>
            <th>姓名</th>
            <th>电话</th>
            <th>邮箱</th>
            <th></th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="customer in filterBy(customers,filterInput)" >
            <td>{{customer.name}}</td>
            <td>{{customer.phone}}</td>
            <td>{{customer.email}}</td>
            <td><router-link v-bind:to="'/customer/'+customer.id" class="btn btn-default">详情</router-link></td>

          </tr>
        </tbody>
      </table>
    </div>
</template>

<script>
  import Alert from './Alert'
    export default {
        name: "customers",
      data(){
          return{
            customers:[],
            alert:'',
            filterInput:'',

          }
      },
      methods:{
        filterBy(customers,value){
          return customers.filter(function (customer) {
            return customer.name.match(value);
          })
        },
          /*fetchCustomers(){
            this.$http.get("http://localhost:3000/users")
              .then(function (response) {
                this.customers = response.body;
              })
          }*/
        fetchCustomers(){
          this.$http.get("http://localhost:3000/users")
            .then( (response)=> {
              this.customers = response.data;
            })
        }
      },
      created(){
        if(this.$route.query.alert){
          this.alert = this.$route.query.alert;
        }
        this.fetchCustomers();

      },
      updated(){


            this.fetchCustomers();

      },
      components:{
          Alert
      }


    }
</script>

<style scoped>

</style>
