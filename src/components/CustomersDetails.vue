<template>
  <div class="Details container">
  	<h1 class="page-header">姓名：{{customer.name}}</h1>
  	<ul class="list-group">
  		<li class="list-group-item">电话：<input type="text" v-model="customer.phone"/></li>
  		<li class="list-group-item">邮箱：{{customer.email}}</li>
  	</ul>
  	<ul class="list-group">
  		<li class="list-group-item">学历：{{customer.education}}</li>
  		<li class="list-group-item">毕业学校：{{customer.graduationschool}}</li>
  		<li class="list-group-item">职业：{{customer.profession}}</li>
  		<li class="list-group-item">简介：{{customer.profile}}</li>
  	</ul>
  	<button @click="delet">删除</button>
  	<button @click="edit">编辑</button>
  </div>
</template>

<script>
	import axios from 'axios'
export default {
  name: 'Details',
  data () {
    return {
      customer:{},
      id:'',
      boo:false
    }
  },
  methods:{
  	fetchCustomers(id){
  		axios.get("http://localhost:3000/user/"+id).then((data)=>{
  			console.log(data.data);
  			this.customer = data.data
  		})
  	},
  	delet(){
  		axios.delete("http://localhost:3000/user/"+this.id).then((data)=>{
  			this.$router.push('/');
  		})
  	},
  	edit(e){
  			console.log(123);
				if(!this.customer.name || !this.customer.phone || !this.customer.email){
					console.log('请填写相应信息！')
				}else{
					let newCustomer = {
						name:this.customer.name,
						phone:this.customer.phone,
						email:this.customer.email,
						education:this.customer.education,
						graduationschool:this.customer.graduationschool,
						profession:this.customer.profession,
						profile:this.customer.profile
					}
					
					axios.put("http://localhost:3000/user/"+this.id,newCustomer).then((data)=>{
						console.log(data);
						this.$router.push({path:"/",query:{alert:"用户信息添加成功！"}});
					})
				}
				e.preventDefault();
  	}
  },
  created(){
  	this.fetchCustomers(this.$route.params.id);
  	this.id = this.$route.params.id;
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
