<template >
	<div class="search">
		<label class="">Search</label>
		<input type="text" v-bind:value="value" v-on:input="$emit('input', $event.target.value)" placeholder="Filter Results">
	</div>
</template>

<script>
export default {
	name: 'SearchInput',
	props: [
		'value'
	]
}
</script>
<style scoped lang="scss">
	//Showing the Use of Component Scoped SCSS
	//Passing Component Variable to accept Custom Properties
	$component-padding: --medium;

	.search {
		display: grid;
		grid-template-columns: min-content auto;
		grid-template-areas: "label input";
		padding-bottom: var(--xlarge);
		margin-bottom: var(--xlarge);
		border-bottom: 1px solid var(--tertiary);
		label {
			display: flex;
			align-items: center;
			margin-right: var($component-padding);
		}
	}
</style>
