<template>
  <div id="app">
  	 <myheader></myheader>
    <router-view/>
  </div>
</template>

<script>
	import myheader from './components/Header'
export default {
  name: 'App',
  components:{
  	myheader
  }
}
</script>

<style>

</style>
