<template>

	<div class="map-compare">
		<div class="map-compare__slider">
			<h1 class="map-compare__title">
				<strong>Map</strong>Compare</h1>
			<h4 class="slider__title hide-for-medium-up">Daily requests</h4>
			<div class="slider">
				<h5 class="slider__title hide-for-small-only">Daily requests</h5>
				<span class="slider__from">{{views.min}}</span>
				<div class="slider__range input--range" :style="`--current: ${views.current / views.max * 100} `">
					<input type="range" v-model="views.current" :min="views.min" :max="views.max" :step="views.step" />
					<div class="slider__current-panel">
						<span class="slider__current">{{views.current}}</span>
					</div>
				</div>
				<span class="slider__till">{{views.max}}</span>
			</div>
		</div>
		<transition-group tag="ul" name="flip-list" class="list map-compare__providers">
			<li class="map-compare__provider provider list-item" v-for="(provider,index) in orderedProviders" :key="index" :class="{'map-compare__provider--free': views.current < provider.free}">
				<div class="provider__title">
					<h3>{{provider.name}}</h3>
				</div>
				<div class="provider__price">
					<h4 v-if="calcPrice(provider) > 0">$ {{calcPrice(provider) }}</h4>
					<h4 v-else>free</h4>
				</div>
			</li>
		</transition-group>

	</div>
</template>

<script>
export default {
	data() {
		return {
			views: {
				min: 0,
				step: 1000,
				max: 1000000,
				current: 0
			},
			providers: [
				{
					name: 'Google Maps',
					free: 25000,
					currentPrice: 0,
					pricing: [{ price: 0.5, limit: 1000, per: 1000 }]
				},
				{
					name: 'Apple Maps',
					free: 250000,
					currentPrice: 0,
					pricing: [{ price: 0.5, limit: 1000, per: 1000 }]
				},
				{
					name: 'Mapbox',
					free: 50000 / 30,
					currentPrice: 0,
					pricing: [{ price: 0.5, limit: 1000, per: 1000 }]
				},
				{
					name: 'Bing',
					free: 10000,
					currentPrice: 0,
					pricing: [{ price: 0.5, limit: 1000, per: 1000 }]
				},
				{
					name: 'Mapfit',
					free: 50000 / 30,
					currentPrice: 0,
					pricing: [
						{ price: 0.5, limit: 150000, per: 1000 },
						{ price: 0.2, limit: 1000000, per: 1000 }
					]
				},
				{
					name: 'Yandex',
					free: 30000 / 30,
					currentPrice: 0,
					pricing: [
						{ price: 1.77, limit: 1000, per: 1000 },
						{ price: 0.53, limit: 10000, per: 1000 },
						{ price: 0.35, limit: 25000, per: 1000 },
						{ price: 0.25, limit: 50000, per: 1000 },
						{ price: 0.16, limit: 100000, per: 1000 }
					]
				}
			],
			orderedProviders: []
		};
	},
	mounted() {
		this.orderProviders();
	},
	methods: {
		orderProviders() {
			this.orderedProviders = _.orderBy(this.providers, 'currentPrice');
		},
		calcPrice(provider) {
			let _this = this;
			let price = 0;
			provider.pricing.forEach(function(limit) {
				if (_this.views.current > limit.limit) {
					price =
						(_this.views.current - provider.free) * (limit.price / limit.per);
				}
			});
			if (price < 0) {
				price = 0;
			}
			provider.currentPrice = price;
			return Math.round(price * 100) / 100;
		}
	},

	watch: {
		views: {
			handler: function(value) {
				this.orderProviders();
			},
			deep: true
		}
	}
};
</script>

<style lang="scss">
@import './assets/scss/vars';
@import '~piet';

.hide-for-small-only {
	@media #{$small-only} {
		display: none;
	}
}
.hide-for-medium-up {
	@media #{$medium-up} {
		display: none;
	}
}
.testlist {
	display: flex;
	flex-direction: column;
	li {
		display: inline-block;
	}
}
/** demo11 **/
.flip-list-move {
	transition: transform 1s;
}
@keyframes comeIn {
	from {
		transform: translateY(100%);
		opacity: 0;
	}
	to {
		transform: translateY(0%);
		opacity: 1;
	}
}
.map-compare {
	width: 640px;
	max-width: 80vw;
	padding: 10vh 30px 30px 30px;
	overflow: hidden;
	margin: auto;
	@media #{$small-only} {
		padding-top: 0;
		max-width: 100vw;
		padding: 0 30px 30px 30px;
	}
	&__title {
		color: color(Pink);
		strong {
			color: color(Black);
		}
		@media #{$small-only} {
			background-color: color(Black);
			width: calc(100% + 60px);
			margin-left: -30px;
			color: color(White);
			padding: 2rem;
			color: color(Pink);
			strong {
				color: color(White);
			}
		}
	}
	&__slider {
	}
	&__providers {
		width: 100%;
		// display: flex;
		// flex-wrap: wrap;
		// flex-direction: column;
		counter-reset: provider;
	}
	&__provider {
		transform: translateY(100%);
		@for $i from 1 through 10 {
			&:nth-child(#{$i}) {
				animation: comeIn 0.3s #{$i/10}s cubic-bezier(0, 1.3, 1, 1.18) forwards;
			}
		}
		width: 100%;
		counter-increment: provider;
		position: relative;

		padding: 2rem;
		// display: inline-block;
		background-color: color(White, 1);
		transition: background 0.3s ease-in-out, box-shadow 0.3s ease-in-out;
		background-size: 100% 200%;
		background-position: 50% 0;
		box-shadow: 0 -4px 0 0 color(lightBlue) inset,
			0 0.5rem 1rem 0 color(Black, 0.1);
		border-radius: 4px;
		justify-content: space-between;
		& + .map-compare__provider {
			margin-top: 1rem;
		}
		background-image: linear-gradient(
			to bottom,
			color(Green, 0) 50%,
			color(Green, 0.1),
			color(Green, 0.3)
		);
		&:before {
			position: absolute;
			left: 0;
			top: 50%;
			transform: translate(-50%, -50%);
			background-color: color(lightBlue);
			border-bottom: 2px solid darken(lightBlue, 10%);
			display: block;
			border-radius: 50%;
			width: 2rem;
			height: 2rem;
			text-align: center;
			line-height: 1.75rem;
			font-weight: bold;
			content: counter(provider);
			box-shadow: 0 0.5rem 1rem 0 color(Black, 0.1);
		}
		&--free {
			background-color: color(White, 1);
			box-shadow: 0 -4px 0 0 color(lightGreen) inset,
				0 0.5rem 1rem 0 color(Black, 0.1);
			background-position: 0% 0;
			&:before {
				background-color: color(lightGreen);
				border-bottom: 2px solid darken(lightGreen, 15%);
			}
		}
	}
}
.provider {
	&__price {
		font-weight: bold;
		font-size: 0.875rem;
		text-transform: uppercase;
	}
}
.slider {
	display: flex;
	position: relative;
	z-index: 10;
	@media #{$small-only} {
		width: calc(100% + 2rem);
		margin-left: -1rem;
	}
	&__title {
		flex-shrink: 0;
		padding: 1rem 1rem 1rem 0;
		line-height: 1.75rem;
	}
	&__from,
	&__till {
		font-size: 1rem;
		line-height: 2rem;
		display: block;
		padding: 1rem;
		font-weight: bold;
	}
	&__range {
		width: 100%;
		position: relative;
		input {
			width: 100%;
		}
	}
	&__current-panel {
		position: absolute;
		left: 0.5rem;
		width: calc(100% - 1rem);
		top: 100%;
		pointer-events: none;
		transform: translateX(calc(var(--current) * 1%));
	}
	&__current {
		position: absolute;
		left: 0%;
		top: 50%;
		background-color: color(Pink);
		padding: 0.75rem 1rem;
		border-radius: 5px;
		transform: translateX(-50%) translateY(-0.5rem);
		border-bottom: 2px solid darken(Pink, 10%);
		font-weight: bold;
		font-size: 0.8rem;
		box-shadow: 0 0.25rem 0.5rem 0 color(Black, 0.1);
		&:before {
			content: '';
			width: 0.75rem;
			height: 0.75rem;
			background-color: color(Pink);
			position: absolute;
			border-radius: 4px 0 0 0;
			left: 50%;
			top: 0;
			transform: translate(-50%, -50%) rotate(45deg);
		}
	}
}
</style>
