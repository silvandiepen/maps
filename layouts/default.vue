<template>
	<div class="layout">
		<reload></reload>
		<nuxt/>
	</div>
</template>
<script>
import reload from '~/components/reload.vue';
export default { components: { reload } };
</script>

<style lang="scss">
@import './assets/scss/vars';
@import '~piet';
.layout {
	overflow: visible;
}
.page {
	position: relative;
	z-index: 1;
}
</style>

