<template>
	<div id="app" class="training">
		<div class="form-group row">
			<h2 class="col ">Тренажер. Уровень {{ level + 1 }}</h2>
			<select class="form-control col" style="width: 50px" v-model.number="level">
				<option v-for="(item, index) in levels" :value="index">{{item.name}}</option>
			</select>
		</div>
		<hr> 
		<div class="progress">
			<div class="progress-bar" :style="progressStyles"></div>
		</div>
		<div class="box my-1">
			<AppFunctionTest v-if="state == 'test'"></AppFunctionTest>
			<transition name="flip" mode="out-in">

				<AppStartScreen 
				v-if="state == 'start'" 
				@onStart="onStart" 
				></AppStartScreen>

				<AppQuestion 
				v-else-if="state == 'question'" 
				@success="onQuestSuccess"
				@error="onQuestError"
				@saveData="saveData"
				:settings="levels[level]"
				:questData="questData"
				></AppQuestion>

				<AppMessage
				v-else-if="state == 'message'"
				:type="message.type"
				:text="message.text"
				@onNext="onNext"
				></AppMessage>

				<AppResultScreen
				v-else-if="state == 'result'"
				:stats="stats"
				@repeat="onStart"
				@nextLevel="onNextLevel"
				></AppResultScreen>

				<div v-else>
					Unknown state
				</div>

			</transition>
		</div>
	</div>
</template>

<script>
	import AppMessage from './components/Message.vue'
	import AppQuestion from './components/Question.vue'
	import AppStartScreen from './components/StartScreen.vue'
	import AppResultScreen from './components/ResultScreen.vue'
	import AppFunctionTest from './components/FunctionTest.vue'
	import 'bootstrap/dist/css/bootstrap.min.css'
	export default {
		components:{
			AppMessage,
			AppQuestion,
			AppStartScreen,
			AppResultScreen,
			AppFunctionTest,
		},
		data () {
			return {
				state: 'start',
				stats: {
					success: 0,
					error: 0
				},
				message: {
					type: '',
					text: ''
				},
				questData: [],
				questMax: 10,
				level: 0,
				levels: [
				{
					name: 1,
					a:[2, 9],
					b:[2, 2],
					c:[4, 10],
					range: 1,
					variants: 3
				},
				{
					name: 2,
					a:[2, 9],
					b:[2, 3],
					c:[4, 10],
					range: 1,
					variants: 3
				},
				{
					name: 3,
					a:[2, 9],
					b:[2, 4],
					c:[4, 10],
					range: 1,
					variants: 3
				},
				{
					name: 4,
					a:[2, 9],
					b:[2, 5],
					c:[4, 10],
					range: 1,
					variants: 3
				},
				{
					name: 5,
					a:[2, 9],
					b:[2, 6],
					c:[4, 10],
					range: 1,
					variants: 3
				},
				{
					name: 6,
					a:[2, 9],
					b:[2, 7],
					c:[4, 10],
					range: 1,
					variants: 3
				},
				{
					name: 7,
					a:[2, 9],
					b:[2, 8],
					c:[4, 10],
					range: 1,
					variants: 3
				},
				{
					name: 8,
					a:[2, 9],
					b:[2, 9],
					c:[4, 10],
					range: 1,
					variants: 3
				},
				]
			}
		},
		computed: {
			questDone(){
				return this.stats.success + this.stats.error;
			},
			progressStyles(){
				return {
					width: (this.questDone / this.questMax * 100) + '%'
				};
			}
		},
		methods: {
			onStart(){
				this.state = 'question';
				this.stats.success = 0;
				this.stats.error = 0;

			},
			onQuestSuccess(){
				this.state = 'message';
				this.message.text = 'Отличная работа!';
				this.message.type = 'success';
				this.stats.success++;
			},
			onQuestError(msg){
				this.state = 'message';
				this.message.text = msg;
				this.message.type = 'danger';
				this.stats.error++;
			},
			onNext(){
				if(this.questDone < this.questMax){
					this.state = 'question';
				}else{
					this.state = 'result';
				}
			},
			onNextLevel(){
				this.level++;
				this.onStart();
			},
			saveData(data){
				this.questData.push(data) 
			}


		}
	}
</script>

<style>

</style>
<style scoped>
	.training{
		max-width: 700px;
		margin: 20px auto;
	}
	.flip-enter{

	}
	.flip-enter-active{
		animation: flipInX 0.3s linear;

	}
	.flip-leave-active{
		animation: flipOutX 0.3s linear;

	}
	.progress-bar{
		transition: width 0.5s;
	}

	@keyframes flipInX{
		from{transform: rotateX(90deg);}
		to{transform: rotateX(0deg);}
	}
	@keyframes flipOutX{
		from{transform: rotateX(0deg);}
		to{transform: rotateX(90deg);}
	}
</style>
