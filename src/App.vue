<template>
	<header class="header"><h1>Список заведений</h1></header>

	<div class="btn-wrapper">
		<button class="btnSelect" @click="getRandomPlace(places.length)">
			Выбрать случайное место
		</button>
		<button class="btnSelect" @click="toogle = !toogle" v-if="!toogle">
			Вернуться ко всем местам
		</button>
	</div>

	<div class="wrapper-places" v-if="this.places.length !== 0">
		<Place :places="places" v-if="toogle" />
		<Place :places="randomPlace" v-else />
	</div>
	<div class="loading" v-else>Loading...</div>
</template>

<script>
import Place from '@/components/Place.vue';

export default {
	components: {
		Place,
	},
	data() {
		return {
			places: [],
			randomPlace: [],
			toogle: true,
		};
	},
	methods: {
		fetchPlaces() {
			fetch('https://bandaumnikov.ru/api/test/site/get-index')
				.then((res) => res.json())
				.then((res) => res.data)
				.then((res) => (this.places = res));
		},
		getRandomPlace(max) {
			this.randomPlace = [];
			const random = Math.floor(Math.random() * max);
			this.randomPlace.push(this.places[random]);
			this.toogle = false;
		},
	},
	mounted() {
		this.fetchPlaces();
	},
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Open+Sans:wght@300&display=swap');

* {
	font-family: 'Open Sans', sans-serif;
	box-sizing: border-box;
}
.header {
	text-align: center;
	color: grey;
}
.btn-wrapper {
	display: flex;
	justify-content: center;
}
.btnSelect {
	display: block;
	margin: 20px;
	background: none;
	border: none;
	border-radius: 10px;
	box-shadow: rgba(0, 0, 0, 0.1) 0px 4px 12px;
	width: 200px;
	height: 50px;
}
.wrapper-places {
	display: flex;
	flex-wrap: wrap;
	justify-content: center;
}
.loading {
	text-align: center;
	font-size: 30px;
}
</style>
