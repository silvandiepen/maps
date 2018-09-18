<template>
	<transition-group class="map-compare__providers" name="flip-list" tag="div">
		<div class="map-compare__provider" v-for="item in newProviders" v-bind:key="item" @click="incrPrice(item)">
			<p>{{ item.name }}</p>
			<p>{{ item.currentPrice }}</p>
		</div>
	</transition-group>
</template>

<script>
export default {
	data() {
		return {
			items: [1, 2, 3, 4, 5, 6, 7, 8, 9],
			newProviders: [],
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
			]
		};
	},
	computed: {
		orderedProviders: function() {
			return _.orderBy(this.providers, 'currentPrice');
		}
	},
	methods: {
		randomIndex: function() {
			return Math.floor(Math.random() * this.items.length);
		},
		shuffle: function() {
			this.providers = _.shuffle(this.providers);
		},
		incrPrice(item) {
			item.currentPrice = item.currentPrice + 1;
		}
	},
	mounted() {
		let _this = this;
		// setInterval(function() {
		// 	_this.shuffle();
		// }, 2000);
	}
};
</script>

<style>
/** demo11 **/
.flip-list-move {
	transition: transform 1s;
}
.listitem {
	display: block;
}
</style>