<template>
	<p>{{this.firstItemOnPage}} - {{this.lastItemOnPage}} of {{this.totalItems}}</p>
	
</template>
<script lang="ts">
import { defineComponent, ref } from 'vue'
export default defineComponent({
	name: 'PaginationNumbers',
	props: {
		currentPage : {
			type: Number,
			required: true
		},
		maxPages : {
			type: Number,
			required: true
		},
		itemsPerPage: {
			Type: Number,
			required: true,
		},
		totalItems: {	
			Type: Number,
			required: true,
		}
	},
	computed: {
		firstItemOnPage: function () {
			var lowBound = this.currentPage * this.itemsPerPage
			lowBound = lowBound - this.itemsPerPage
			return lowBound
		},
		lastItemOnPage: function () {
			if (this.firstItemOnPage + (this.itemsPerPage - 1) <= this.totalItems) {
				return this.firstItemOnPage + (this.itemsPerPage - 1)
			}else {
				return this.totalItems
			}
			
		}
	}
})
	
</script>
<style lang="scss" scoped>
	p {
		color: rgba(0, 0, 0, 0.45);
	}
</style>