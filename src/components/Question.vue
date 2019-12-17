<template>
	<div class="alert" role="alert">

		<h3>{{ curEx }} = ?</h3>
		<hr>

		<div class="buttons"> 
			<button class="btn btn-success mx-2" 
				v-for="number in answers" 
				@click="onAnswer(number); $emit('saveData', curEx)"
			>
				{{ number }}
			</button>
		</div>

	</div>	
</template>



<script>
	export default {
		props: ['settings', 'questData'],
		data(){
			// let a = mtRand(this.settings.from, this.settings.to);
			// let b = mtRand(this.settings.from, this.settings.to - a);
			let a, b, c, x, count = 0, isNotRepeat = true, curEx;

			// let test=0;
			// let testArr = [];
			// while(test < 100){
			// 	testArr.push(mtRand(1,9));
			// 	test++
			// }
			// testArr.sort(function(a, b){
			// 	return a - b
			// })
			// console.log(testArr);
			this.settings.a.sort(function(a, b){
				return a - b;
			})
			this.settings.b.sort(function(a, b){
				return a - b;
			})
			while(isNotRepeat && count < 10){
				a = mtRand(this.settings.a[0], this.settings.a[1]);
				b = mtRand(this.settings.b[0], this.settings.b[1]);

				x = a;
				a = a > b ? a : b;
				b = b < x ? b : x;

				c = a + b; 
				curEx = a + '﹒' + b;
				isNotRepeat = this.questData.indexOf(curEx) > -1 ? true : false;
				count++
			}
			return {
				a: a > b ? a : b, 
				b: b < a ? b : a,
				c: isNotRepeat,
				curEx: curEx,
			} 
		},
		computed: {
			good(){
				return this.a * this.b;
			},
			answers(){
				let res = [this.good]

				while(res.length < this.settings.variants){
					let num = mtRand(this.good - this.settings.range, this.good + this.settings.range);

					if(res.indexOf(num) === -1){
						res.push(num);
					}
				}
				return res.sort(function(){
					return Math.random() > 0.5;
				});
			}
		},
		methods: {
			onAnswer(num){
				if(num == this.good){
					this.$emit('success');
				}else{
					this.$emit('error', `${this.a} + ${this.b} = ${this.good} !`)
				}
			}
		}
	}
	function mtRand(min, max){
		let diff = max - min;
		return min == max ? min : Math.floor(Math.random() * (diff + 1)) + min;
	}
	function random(min, max){
		let a = mtRand(min, max);
		let b = mtRand(min, max);
		let arr1 = [a, b];
		arr1.sort(function(a, b){
			return a + b
		});
		return {a: a, b: b}
	}
	// function mtRand(min, max){
	// 	let diff = max - min;
	// 	return Math.floor(Math.random() * (diff + 1)) + min;
	// }
</script>



<style scoped>
	.alert{
		padding-top: 30px;
		background-color: #eee;
	}
	/*.buttons{
		display: flex;
		justify-content: space-around; 
		justify-content: center;
	}*/
</style>