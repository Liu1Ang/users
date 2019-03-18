<template>
	<div class="add container">
		<h1 class="page-header">添加用户</h1>
		<form @submit="addCustomer">
			<div class="well">
				<h4>用户信息</h4>
				<div class="form-group">
					<label for="xing">姓名</label>
					<input type="text" id="xing" class="form-control" placeholder="确认后不可更改！" v-model="customer.name"/>
				</div>
				<div class="form-group">
					<label for="tell">电话</label>
					<input type="number" id="tell" class="form-control" placeholder="电话" v-model="customer.phone"/>
				</div>
				<div class="form-group">
					<label for="email">邮箱</label>
					<input type="text" id="email" class="form-control" placeholder="邮箱" v-model="customer.email"/>
				</div>
				<div class="form-group">
					<label for="xue">学历</label>
					<input type="text" id="xue" class="form-control" placeholder="学历" v-model="customer.education"/>
				</div>
				<div class="form-group">
					<label for="bi">毕业学校</label>
					<input type="text" id="bi" class="form-control" placeholder="毕业学校" v-model="customer.graduationschool"/>
				</div>
				<div class="form-group">
					<label for="zhi">职业</label>
					<input type="text" id="zhi" class="form-control" placeholder="职业" v-model="customer.profession"/>
				</div>
				<div class="form-group">
					<label>个人简介</label>
					<textarea class="form-control" rows="6" v-model="customer.profile"></textarea>
				</div>
				<button type="submit" class="btn btn-primary">添加</button>
			</div>
		</form>
	</div>
</template>

<script>
	import axios from 'axios'
	export default{
		name:"add",
		data(){
			return{
				customer:{}
			}
		},
		methods:{
			addCustomer(e){
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
					
					axios.post("http://localhost:3000/user",newCustomer).then((data)=>{
						console.log(data);
						this.$router.push({path:"/",query:{alert:"用户信息添加成功！"}});
					})
				}
				e.preventDefault();
			}
		}
	}
</script>

<style>
</style>