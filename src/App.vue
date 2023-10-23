<template>
	<div class="container pt-1">
		<div class="card">
			<h2>Актуальные новости {{ now }}</h2>
			<span>
				Открыто <strong>{{ openRate }}</strong> | Прочитано
				<strong>{{ readRate }}</strong></span
			>
			<app-news
				v-for="item in news"
				:key="item.id"
				:id="item.id"
				:title="item.title"
				:text="item.text"
				:is-open="item.isOpen"
				:was-read="item.wasRead"
				@open-news="openRate++"
				@read-news="readNews"
			></app-news>
		</div>
	</div>
</template>

<script>
	import AppNews from './components/AppNews.vue';
	export default {
		/* name: 'App',
		components: {}, */
		data() {
			return {
				now: new Date().toLocaleDateString(),
				news: [
					{
						title: 'Джо Байден победил на выборах США',
						text: 'Это плохо для Трампа',
						id: 1,
						isOpen: false,
						wasRead: false,
					},
					{
						title: 'Vue 3 успешно работает',
						text: 'Это плохо для React',
						id: 2,
						isOpen: false,
						wasRead: false,
					},
				],
				openRate: 0,
				readRate: 0,
			};
		},

		provide() {
			return {
				// title: 'List of all news',
				news: this.news,
			};
		},

		methods: {
			readNews(id, sign) {
				const idx = this.news.findIndex((news) => news.id === id);
				switch (sign) {
					case '-':
						this.news[idx].wasRead = false;
						this.readRate--;
						break;

					case '+':
						this.news[idx].wasRead = true;
						this.readRate++;
						break;

					default:
						break;
				}
			},
		},

		components: {
			'app-news': AppNews,
		},
	};
</script>

<style>
	h2 {
		color: darkred;
	}
</style>
