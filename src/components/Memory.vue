<template>
	<div>
		Let's play a memory game
		<div>
			<button @click.prevent="start">Let's Start</button>
		</div>
		<div>
			{{display}}
		</div>
		<div>
			<button v-for="word in words" @click.prevent="clicked(word)">{{word}}</button>
		</div>
	</div>
</template>

<script>
	export default {
		name:"memory",
		mounted: function(){
			console.log('mounted stuff')
		},
		methods: {
			start: function(){
				var n= 0;
				
				//Let's start displaying 4 words for half second
			},
			clicked: function(word){
				alert(word)
			}
		},
		data: function(){
			return {
				display:'',
				words:["i",'am','possible','to','create','a','project','methods']
			}
		}

	}
</script>