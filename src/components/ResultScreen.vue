<template>
	<div class="alert alert-primary">
		
		<h3>Правильных: {{ stats.success }}</h3>
		<h3>Ошибок: {{ stats.error }}</h3>
		<hr>
		<button class="btn btn-primary mx-2" @click="$emit('repeat')" >Повторить</button>
		<button class="btn btn-primary mx-2" @click="$emit('nextLevel')" >Следующий уровень</button>

	</div>
</template>

<script>
	export default {
		props: ['stats']
	}
</script>

<style>
	
</style>