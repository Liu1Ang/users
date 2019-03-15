<template>
  <div class="Details container">
    Details
  </div>
</template>

<script>
export default {
  name: 'Details',
  data () {
    return {
      customer:""
    }
  },
  methods:{
  	fetchCustomers(id){
  		axios.get("http://localhost:3000/user").then((data)=>{
  			console.log(data);
  			this.customers = data.data
  		})
  	}
  },
  created(){
  	this.fetchCustomers(this.$route.params.id)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
