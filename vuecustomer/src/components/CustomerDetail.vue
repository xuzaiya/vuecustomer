<template>
    <div class="details container" >
      <router-link to="/" class="btn btn-default">返回主页</router-link>
      <h1 class="page-header">
        {{customer.name}}
        <span class="pull-right">
          <router-link class="btn btn-primary" v-bind:to="'/edit/'+customer.id">编辑</router-link>
          <button class="btn btn-danger" v-on:click="deleteCustomer(customer.id)">删除</button>
        </span>
      </h1>
      <ul class="list-group">
        <li class="list-group-item"><span class="glyphicon glyphicon-asterisk">{{customer.phone}}</span></li>
        <li class="list-group-item"><span class="glyphicon glyphicon-plus">{{customer.email}}</span></li>
      </ul>
      <ul class="list-group">
        <li class="list-group-item"><span class="glyphicon glyphicon-education">{{customer.education}}</span></li>
        <li class="list-group-item"><span class="glyphicon glyphicon-calendar">{{customer.graduationschool}}</span></li>
        <li class="list-group-item"><span class="glyphicon glyphicon-fire">{{customer.profession}}</span></li>
        <li class="list-group-item"><span class="glyphicon glyphicon-hand-right">{{customer.profile}}</span></li>
      </ul>
    </div>
</template>

<script>
    export default {
        name: "customerdetail",
      data(){
          return{
            customer:'',
          }
      },
      methods:{
        //用axios替换vue-resource
          /*fetchCustomers(id){
          this.$http.get("http://localhost:3000/users/"+id)
            .then( function(response){
              this.customer = response.body;
              console.log(this.customer);
            })
        }*/
        fetchCustomers(id){
          this.$http.get("http://localhost:3000/users/"+id)
            .then((response)=>{
              this.customer = response.data;
              console.log(this.customer);
            })
        }

          ,
            /*deleteCustomer(id){
              this.$http.delete("http://localhost:3000/users/"+id)
                .then( function(response) {
                  this.$router.push({path:'/',query:{alert:'用户删除成功'}});
                })
          }
*/

        deleteCustomer(id){
          this.$http.delete("http://localhost:3000/users/"+id)
            .then( (response)=> {
              this.$router.push({path:'/',query:{alert:'用户删除成功'}});
            })
        },

      },
      created(){
          this.fetchCustomers(this.$route.params.id);
      }
    }
</script>

<style scoped>

</style>
