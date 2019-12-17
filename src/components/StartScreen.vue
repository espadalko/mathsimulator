<template>
	<div class="alert alert-secondary">

		<h3>Вы готовы?</h3>
		<button class="btn btn-success" @click="$emit('onStart')"> Старт </button>

	</div>
</template>


<script>
	export default {

	}
</script>


<style>
	.alert{
		text-align: center;
	}	
	h3, .btn{
		margin: 30px 0;
	}
</style>