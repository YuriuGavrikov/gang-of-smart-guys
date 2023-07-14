<template>
	<div
		class="wrapper"
		:class="{ shake: disabled }"
		v-for="place in places"
		:key="place.id"
	>
		<div class="photo">
			<img class="img" :src="place.photo" v-if="place.photo" />
			<img
				class="img"
				src="https://t4.ftcdn.net/jpg/04/70/29/97/360_F_470299797_UD0eoVMMSUbHCcNJCdv2t8B2g1GVqYgs.jpg"
				alt=""
				v-else
			/>
		</div>
		<div class="description">
			<div class="title">
				<b>{{ place.name }}</b>
			</div>
			<hr />
			<div><b>Кухня</b>: {{ place.cuisine }}</div>
			<div><b>Бизнес-ланч</b>: {{ place.business_lunch }}</div>
			<div><b>Средний чек</b>: {{ place.price }} руб</div>
			<div><b>Адрес</b>: {{ place.address }}</div>
			<div><b>Расстояние до</b>: {{ place.distance }} м</div>
			<div><b>Как пройти</b>: {{ place.landmark }}</div>
			<div><b>Время до</b>: {{ place.time }} мин</div>
		</div>
	</div>
</template>

<script>
export default {
	props: {
		places: { type: Array, required: true },
	},
	data() {
		return {
			disabled: false,
		};
	},
	methods: {
		warnDisabled() {
			this.disabled = true;
			setTimeout(() => {
				this.disabled = false;
			}, 1500);
		},
	},
	mounted() {
		this.warnDisabled();
	},
};
</script>

<style scoped>
.wrapper {
	width: 250px;
	display: flex;
	flex-direction: column;
	align-items: center;
	border-radius: 10px;
	margin: 10px;
	box-shadow: rgba(0, 0, 0, 0.1) 0px 4px 12px;
}
.photo {
	width: 100%;
	height: 160px;
	border-radius: 10px 10px 0 0;
}
.img {
	width: 100%;
	height: 100%;
	object-fit: cover;
	border-radius: 9px 9px 0 0;
}
.description {
	width: 100%;
	height: 60%;
	padding: 10px 15px 15px 15px;
	font-size: 12px;
	.title {
		font-size: 18px;
	}
}

/* Animation */
.shake {
	animation: shake 0.7s;
	transform: translateY(0px);
}

@keyframes shake {
	30% {
		transform: translateY(-10px);
	}
}
</style>
