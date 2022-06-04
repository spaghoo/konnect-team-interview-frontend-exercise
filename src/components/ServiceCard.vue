/*using v-if and v-else to render the full name 
and description only if it is less than a 
certain number of characters. 
Settled on 25 and 90 respectively. */

<template>
	<div class="card">
		<div v-if="name.length < 20">
			<h3>{{name}}</h3>
		</div>
		<div v-else>
			<h3>{{name.substring(0,20) + "..."}}</h3>
		</div>
		
		
		<div v-if="description.length < 90">
			<p>{{description}}</p>
		</div>
		<div v-else>
			<p>{{description.substring(0,90) + "..."}}</p>
		</div>
		
		<VersionBubble :versions="versions" />
		
	</div>
	
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'
import VersionBubble from '@/components/VersionBubble.vue'

export default defineComponent({
	name: 'ServiceCard',
	components: {
		VersionBubble,
	},
	props: {
		
		name : {
			type: String,
			required: true,
		},
		description : {
			type: String,
			required: false,
		},
		versions : {
			type: Number,
			required: true,
			default: 1,
		}
	},
	
})
	
	
</script>

<style>
	.card {
		justify-content: space-between;
	}
</style>