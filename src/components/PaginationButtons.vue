<template>
	<div class="buttons">
	<div v-if="direction == true">
		<KIcon icon="arrowLeft" />
	</div>
	<div v-else>
		<KIcon icon="arrowRight" />
	</div>
	</div>
</template>
<script lang="ts">
import { defineComponent } from 'vue'
import { RouterView } from 'vue-router'
import { KIcon } from '@kong/kongponents'
export default defineComponent({
	name: 'PaginationButtons',
	props: {
		direction : {
			type: Boolean,
			required: true,
		}
	},
	components: {
		KIcon,
	}
})	
</script>
<style lang="scss" scoped>
	.buttons {
		background: #FFF;
		border: 1px solid #1456CB;
		-webkit-border-radius: 50%;
		color: #1456CB;
		font-weight: bold;
		text-align: center;
		line-height: 2;
		width: 30px;
	}
	
	
</style>