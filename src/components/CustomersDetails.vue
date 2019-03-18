<template>
  <div class="Details container">
  	<h1 class="page-header">姓名：{{customer.name}}</h1>
  	<form @submit="nosubmit">
	  	<ul class="list-group">
	  		<li class="list-group-item">电话：<input type="text" :disabled="isdisabled" :class="boo?'':'active'" v-model="customer.phone"/></li>
	  		<li class="list-group-item">邮箱：<input type="text" :disabled="isdisabled" :class="boo?'':'active'" v-model="customer.email"/></li>
	  	</ul>
	  	<ul class="list-group">
	  		<li class="list-group-item">学历：<input type="text" :disabled="isdisabled" :class="boo?'':'active'" v-model="customer.education"/></li>
	  		<li class="list-group-item">毕业学校：<input type="text" :disabled="isdisabled" :class="boo?'':'active'" v-model="customer.graduationschool"/></li>
	  		<li class="list-group-item">职业：<input type="text" :disabled="isdisabled" :class="boo?'':'active'" v-model="customer.profession"/></li>
	  		<li class="list-group-item">简介：<textarea class="form-control" :disabled="isdisabled" rows="6" :class="boo?'':'active'" v-model="customer.profile"></textarea></li>
	  	</ul>
	  	<button @click="delet">删除</button>
	  	<button v-if="isedit" @click="edit">编辑</button>
	  	<button v-if="!isedit" @click="editdetails">确认</button>
  	</form>
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
      boo:false,
      active:'active',
      isedit:true,
      isdisabled:true
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
  	edit(){
  		this.isedit = false;
  	},
  	nosubmit(e){
  		e.preventDefault();
  		this.boo = true;
  		this.isdisabled = false
  	},
  	editdetails(e){
//			console.log(123);
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
						this.$router.push({path:"/",query:{alert:"用户信息修改成功！"}});
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
	.active{
		border-width: 0 !important;
	}
	input:disabled{
		background: transparent !important;
	}

</style>
