<template>
	<section class="intro">
		<!-- <h1>Map Compare</h1> -->
		<map-compare></map-compare>
	</section>
</template>

<script>
import MapCompare from '~/components/MapCompare.vue';
export default {
	components: {
		MapCompare
	},
	data() {
		return {
			data: [
				{
					provider: 'Google Maps',
					apis: [
						{
							name: 'Android SDK',
							free: 150000,
							remark: 'After ID verification'
						},
						{
							name: 'iOS SDK',
							free: 150000,
							remark: 'After ID verification'
						},
						{
							name: 'Maps JavaScript API',
							free: 25000,
							price: 0.5,
							per: 1000
						},
						{
							name: 'Maps static API',
							free: 25000,
							price: 0.5,
							per: 1000
						},
						{
							name: 'Street View API',
							free: 25000,
							price: 0.5,
							per: 1000
						},
						{
							name: 'Embed API',
							free: 25000,
							price: 0.5,
							per: 1000
						},
						{
							name: 'Directions API',
							free: 2500,
							price: 0.5,
							per: 1000
						},
						{
							name: 'Distance Matrix API',
							free: 2500,
							price: 0.5,
							per: 1000
						},
						{
							name: 'Elevation API',
							free: 2500,
							price: 0.5,
							per: 1000
						},
						{
							name: 'Geocoding API',
							free: 2500,
							price: 0.5,
							per: 1000
						},
						{
							name: 'Geolocation API',
							free: 2500,
							price: 0.5,
							per: 1000
						},
						{
							name: 'Roads API',
							free: 2500,
							price: 0.5,
							per: 1000
						},
						{
							name: 'Time Zone API',
							free: 2500,
							price: 0.5,
							per: 1000
						},
						{
							name: 'Places',
							free: 150000,
							price: 0.5,
							per: 1000,
							remark: 'After ID verification'
						}
					]
				}
			]
		};
	}
};
</script>

<style lang="scss">
@import '~piet';
</style>

