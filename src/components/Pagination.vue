<template >
	<div class="pagination">
		<a v-on:click="$emit('prevPage')" id="btn_prev" class="prev">Prev</a>
		<span id="page"></span>
		<a v-on:click="$emit('nextPage')" id="btn_next" class="next">Next</a>
	</div>
</template>

<script>
export default {
	name: 'Pagination'
}
</script>
<style scoped lang="scss">
	//Showing the Use of Component Scoped SCSS
	.pagination {
		display: flex;
		justify-content: center;
		align-items: center;
		margin: var(--large) 0;
		font-family: "Noto Sans", sans-serif;
		font-size: 0.781rem;
		letter-spacing: 0.15rem;
		line-height: 19px;
		.next {
			margin-left: var(--medium);
			cursor: pointer;
		}
		.prev {
			margin-right: var(--medium);
			cursor: pointer;
		}
	}
</style>
