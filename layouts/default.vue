<template>
	<div class="layout">
		<div class="reload"></div>
		<nuxt/>
	</div>
</template>

<style lang="scss">
@import './assets/scss/vars';
@import '~piet';
.reload {
	width: 100px;
	height: 100px;
	position: fixed;
	left: 50%;
	top: 0;
	transform: translateX(-50%);
	&:before {
		content: '';
		width: 50%;
		height: 50%;
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%) rotate(0deg);
		display: block;
		border: 2px solid #7f7f7f;
		border-radius: 50%;
		border-bottom: 2px solid color(Pink);
		border-top: 2px solid color(lightBlue);
		border-left: 2px solid color(lightGreen);
		animation: rotating 1s linear infinite;
	}
}
@keyframes rotating {
	from {
		transform: translate(-50%, -50%) rotate(0deg);
	}
	to {
		transform: translate(-50%, -50%) rotate(360deg);
	}
}
.layout {
	overflow: visible;
}
.page {
	position: relative;
	z-index: 1;
}
</style>

