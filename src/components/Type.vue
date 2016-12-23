<template>
	<div>
		<div class="fire">
		<div v-for="n in 10" style="margin-to"1 >
		<span class="circle">
			
			{{n}}
		</span>
		</div>
		</div>
		<div class="counter">
			Do the counter attack.
		</div>
	</div>
</template>

<script>
	export default{
		name:'type',
		data: function(){
			return {}
		}
	}
</script>

<style>
	.fire{
		    width: 90%;
    height: 100%;
    position: absolute;
    border-right: 2px black solid;
	}
	.counter{
		    width: 9%;
    height: 100%;
    position: absolute;
    right:0px;
	}
	.circle{
		padding: 5px;
		border-radius: 50%;
		border:1px solid black;
	}
</style>