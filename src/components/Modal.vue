<template >
	<div class="overlay" v-on:click="$emit('closeModal')">
		<div class="image-detail-container">
			<div class="image-detail-card">
				<span class="close" v-on:click="$emit('closeModal')"><img src="../assets/cancel.svg" alt=""></span>
				<h1>{{image.title}}</h1>
				<div class="image-title">
					<label>Title</label><input type="text">
				</div>
				<div class="image-description">
					<label>Description</label><textarea id="image-description" name="image-description"></textarea>
				</div>
				<div class="image-properties">
					<div class="public-domain">
						<label class="label--checkbox">
							<span>Public Domain</span><input value="" type="checkbox">
						</label>
					</div>
					<div class="owner-name">
						<span>Owner Name:</span><span>{{image.ownername}}</span>
					</div>
					<div class="image-dimensions">
						<span>Image Dimensions:</span><span>{{image.width_sq}} x {{image.height_sq}}</span>

					</div>
				</div>
				<div class="cta">
					<button class="button button-cancel">
						<div class="button-label">Cancel</div>
					</button>
					<button class="button button-save">
						<div class="button-label">Save</div>
					</button>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	name: 'Modal',
	props: ['image']
}
</script>
<style scoped lang="scss">

</style>
