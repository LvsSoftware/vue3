<template>
	<div class="card">
		<h3>{{ title }}</h3>
		<app-button @action="open">{{
			isNewsOpen ? 'Закрыть' : 'Открыть'
		}}</app-button>
		<app-button
			color="danger"
			v-if="wasRead"
			@action="mark('-')"
			>Пометить непрочитанным
		</app-button>

		<div v-if="isNewsOpen">
			<hr />
			<p>
				{{ text }}
			</p>

			<app-button
				v-if="!wasRead"
				color="primary"
				@action="mark('+')"
				>Прочесть новость
			</app-button>
			<app-news-list></app-news-list>
		</div>
	</div>
</template>

<script>
	import AppButton from './AppButton.vue';
	import AppNewsList from './AppNewsList.vue';
	export default {
		//props: ['title'],
		emits: {
			'open-news': null,
			'read-news'(id) {
				if (id) {
					return true;
				} else {
					return console.warn('No parameter "id" for emit "read-news"');
				}
			},
		},
		props: {
			title: {
				type: String,
				required: true,
			},
			text: String,
			id: {
				type: Number,
				required: true,
			},
			isOpen: {
				type: Boolean,
				required: false,
				default: false,
			},
			wasRead: Boolean,
		},
		data() {
			//console.log('wasRead', this.wasRead);
			return {
				isNewsOpen: this.isOpen,
			};
		},
		methods: {
			open() {
				this.isNewsOpen = !this.isNewsOpen;
				if (this.isNewsOpen) {
					this.$emit('open-news');
				}
			},
			mark(sign) {
				this.isNewsOpen = false;
				this.$emit('read-news', this.id, sign);
			},
			/* unmark() {
				this.isNewsOpen = true;
				this.$emit('inread-news', this.id);
			}, */
		},
		components: {
			AppButton,
			AppNewsList,
		},
	};
</script>
