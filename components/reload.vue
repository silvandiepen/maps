<template>
	<div class="reload" :class="{'reload--active' : scrolling, 'reload--reload' : reloading}"></div>
</template>
<script>
export default {
	data() {
		return {
			reloading: false,
			scrolling: false
		};
	},
	mounted() {
		let _this = this;
		if (process.browser) {
			window.addEventListener('scroll', function(e) {
				let timer;
				if (window.scrollY < 0) {
					_this.scrolling = true;
					timer = setTimeout(function() {
						_this.reloading = true;
						document.querySelector('.page').classList.add('fadeOut');
						setTimeout(function() {
							location.reload();
						}, 500);
					}, 2000);
				} else {
					_this.scrolling = false;
					clearTimeout(timer);
				}
			});
		}
	}
};
</script>

<style lang="scss">
@import './assets/scss/vars';
@import '~piet';

.page {
	filter: blur(0px);
	opacity: 1;
	transition: filter 0.4s, opacity 0.4s;
	&.fadeOut {
		opacity: 0.5;
		filter: blur(20px);
	}
}
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
		transform: translate(-50%, -50%) scale(0) rotate(0deg);
		display: block;
		transition: transform 0.3s;
		border: 2px solid #7f7f7f;
		border-radius: 50%;
		border-bottom: 2px solid color(Pink);
		border-top: 2px solid color(lightBlue);
		border-left: 2px solid color(lightGreen);
	}
	&--active {
		&:before {
			transform: translate(-50%, -50%) scale(1) rotate(0deg);
			animation: rotating 1s 0.3s linear infinite;
		}
	}
	&--reload {
		&:before {
			animation: reload 0.3s ease-in-out once;
		}
	}
}
@keyframes rotating {
	from {
		transform: translate(-50%, -50%) scale(1) rotate(0deg);
	}
	to {
		transform: translate(-50%, -50%) scale(1) rotate(360deg);
	}
}
@keyframes reload {
	from {
		opacity: 1;
		transform: translate(-50%, -50%) scale(1) rotate(0deg);
	}
	to {
		opacity: 0;
		transform: translate(-50%, -50%) scale(2) rotate(0deg);
	}
}
</style>