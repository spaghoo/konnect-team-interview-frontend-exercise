<template>
	<div class="version-bubble-total">
		<div class="version-bubble">
			
			<p>{{versions}}</p>
			
		</div>
		
		<p class="version-bubble-text">Versions</p>
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

<style lang="scss" scoped>
	.version-bubble {
		
		background: #FFF;
		border: 1px solid #1456CB;
		-webkit-border-radius: 40%;
		color: #1456CB;
		font-weight: bold;
		text-align: center;
		line-height: 0;
		width: 30px;
		position: absolute;
		
	}
	
	.version-bubble-total {
		display: flex;
		align-items: center;
		
		justify-content: space-between;
	}
	
	.version-bubble-text {
		padding: 0px 45px;
	}
	
</style>