<template>
	<div class="card">
		<div v-if="name.length < 25">
			<h3>{{name}}</h3>
		</div>
		<div v-else>
			<h3>{{name.substring(0,25) + "..."}}</h3>
		</div>
		
		
		<div v-if="description.length < 85">
			<p>{{description}}</p>
		</div>
		<div v-else>
			<p>{{description.substring(0,85) + "..."}}</p>
		</div>
		
	</div>
	
</template>

<script>
export default {
	props: {
		
		name : {
			type: String,
			required: true,
		},
		description : {
			type: String,
			required: false,
		}
	}
}
	
	
</script>