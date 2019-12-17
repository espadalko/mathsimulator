<template>
	<div class="alert alert-danger">
		<h3 class="w-100 text-center">FunctionTest</h3>
		<div class="">
			{{ log }}
		</div>
	</div>
</template>


<script>
	export default {
		data(){
			let log = random(2, 2);

			function random(x, n){
				let arr = [];
				if(n != 1){
					return x * random(x, n-1);
				} else {
					return x;
				}
			}
			return {
				log: log,
			}
		}

	}
</script>


<style>
</style>