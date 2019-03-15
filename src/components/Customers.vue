<template>
  <div class="customers container">
  	<Alert v-if="alert" v-bind:message="alert"></Alert>
  	<h1 class="page-header">用户管理系统</h1>
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
  			<tr v-for="customer in customers">
  				<td>{{customer.name}}</td>
  				<td>{{customer.phone}}</td>
  				<td>{{customer.email}}</td>
  				<td><router-link class="btn btn-default" :to="'/customer/'+customer.id">详情</router-link></td>
  			</tr>
  		</tbody>
  	</table>
  </div>
</template>

<script>
	import axios from 'axios'
	import Alert from './Alert'
export default {
  name: 'customers',
	components:{Alert},
  data () {
    return {
    	customers:[],
    	alert:""
    }
  },
  methods:{
  	fetchCustomers(){
  		axios.get("http://localhost:3000/user").then((data)=>{
  			console.log(data);
  			this.customers = data.data
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
//	this.fetchCustomers();
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
