<template>
	<div class="version-bubble">
		
		<p>{{versions}}</p>
		
	</div>
	
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'

export default defineComponent({
	name: 'VersionBubble',
	props: {
		versions : {
			type: Number,
			required: true,
			default: 1,
		}
	}
})
</script>