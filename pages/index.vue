<template>
	<div>
		<div class="container">
			<h1>Проверка OpenGraph</h1>
			<input type="text" v-model="url" placeholder="Введите URL сайта" class="input-field" />
			<button @click="fetchOpenGraphData()" class="submit-button">Проверить</button>

			<div v-if="showData" class="og-data">
				<div class="og-data-item">
					<img :src="openGraphData.image" alt="OpenGraph Image" class="og-data-image" />
				</div>
				<div class="og-data-item">
					<span class="og-data-value">{{ openGraphData.description }}</span>
				</div>
				<div class="og-data-item">
					<a :href="openGraphData.url" target="_blank" rel="noopener noreferrer" class="og-data-value">{{ openGraphData.url }}</a>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			url: "",
			openGraphData: {},
			showData: false,
			apiKey: "bea3cbe4-4420-44e2-b35b-42134a601f25"
		};
	},
	methods: {
		fetchOpenGraphData() {
			if (!this.url) {
				return;
			}

			const apiUrl = `https://opengraph.io/api/1.1/site/${encodeURIComponent(this.url)}?app_id=${this.apiKey}`;

			fetch(apiUrl)
				.then((response) => response.json())
				.then((data) => {
					this.openGraphData = data.hybridGraph || {};
					this.showData = true;
				})
				.catch((error) => {
					console.error(error);
				});
		}
	}
};
</script>

<style lang="sass" scoped>
.container
  max-width: 600px
  margin: 0 auto
  background-color: #fff
  border-radius: 8px
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1)
  padding: 20px

h1
  font-size: 24px
  margin-top: 0

.input-field
  width: 100%
  padding: 10px
  font-size: 16px
  border-radius: 4px
  border: 1px solid #ddd
  margin-bottom: 10px
  transition: border-color 0.3s

.input-field:focus
  outline: none
  border-color: #4267b2

.submit-button
  background-color: #4267b2
  color: #fff
  font-size: 16px
  border: none
  border-radius: 4px
  padding: 10px 20px
  cursor: pointer
  transition: background-color 0.3s

.submit-button:hover
  background-color: #385898

.og-data
  margin-top: 20px

.og-data-item
  margin-bottom: 10px

.og-data-value
  word-break: break-all

.og-data-image
  max-width: 100%
</style>
