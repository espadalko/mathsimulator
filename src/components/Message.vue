<template>
	<div class="alert" :class="'alert-' + type">

		<h3>{{ text }}</h3>
		<hr>

		<div class="buttons mt-1"> 
			<button class="btn btn-primary mx-2" 
					@click="$emit('onNext')"
			>
				Продолжить
			</button>
		</div>

	</div>	
</template>

<script>
	export default {
		props: ['type', 'text']

	}
	
</script>

<style>
	
</style>