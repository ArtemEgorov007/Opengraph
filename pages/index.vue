<template>
	<div class="open-graph">
		<div class="open-graph__container">
			<div class="open-graph__intrormation">
				<h1 class="open-graph__title">Проверь свой <span class="open-graph__title-gradient">Open Graph</span></h1>

				<p class="open-graph__subtitle">
					OpenGraph-карточка, сниппет или превью — это карточка с заголовком, изображением и описанием для ссылки. Она автоматически формируется, когда вы
					делитесь ссылкой в соцсетях.
				</p>

				<a class="open-graph__more-information" href="#">Больше информации об опенграфе</a>
			</div>

			<div class="open-graph__actions">
				<a class="open-graph__link" href="#">Проверить ссылку</a>
				<a class="open-graph__link" href="#">Проверить картинку</a>
			</div>

			<div class="open-graph__form">
				<div class="open-graph__input-wrapper">
					<input type="text" v-model="url" placeholder="http://названиесайта.ru" class="open-graph__input-field" />
					<button @click="fetchOpenGraphData()" class="open-graph__submit-button">Проверить</button>
				</div>
			</div>

			<div class="open-graph__result">
				<h2 class="open-graph__result-title">Результат</h2>

				<div class="open-graph__result-nav">
					<nav class="open-graph__result-nav-menu">
						<ul class="open-graph__result-nav-list">
							<li class="open-graph__result-nav-item">
								<a class="open-graph__result-nav-link" href="#">Facebook</a>
							</li>
							<li class="open-graph__result-nav-item">
								<a class="open-graph__result-nav-link" href="#">Вконтакте</a>
							</li>
							<li class="open-graph__result-nav-item">
								<a class="open-graph__result-nav-link" href="#">Twitter</a>
							</li>
							<li class="open-graph__result-nav-item">
								<a class="open-graph__result-nav-link" href="#">LinkedIn</a>
							</li>
							<li class="open-graph__result-nav-item">
								<a class="open-graph__result-nav-link" href="#">Telegram</a>
							</li>
							<li class="open-graph__result-nav-item">
								<a class="open-graph__result-nav-link" href="#">Telegram</a>
							</li>
							<li class="open-graph__result-nav-item">
								<a class="open-graph__result-nav-link" href="#">WhatsApp</a>
							</li>
							<li class="open-graph__result-nav-item">
								<a class="open-graph__result-nav-link" href="#">Viber</a>
							</li>
						</ul>
					</nav>
				</div>
			</div>
		</div>

		<div v-if="showData" class="open-graph__data">
			<div class="open-graph__data-content">
				<div class="open-graph__data-item">
					<img :src="openGraphData.image" alt="OpenGraph Image" class="open-graph__data-image" />
				</div>
				<div class="open-graph__data-item-wrapper">
					<div class="open-graph__data-item">
						<span class="open-graph__data-value">{{ openGraphData.description }}</span>
					</div>
					<div class="open-graph__data-item">
						<a :href="openGraphData.url" target="_blank" rel="noopener noreferrer" class="open-graph__data-value-link">{{ openGraphData.url }}</a>
					</div>
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

@import url('https://fonts.cdnfonts.com/css/gilroy-bold')
@import '/assets/css/style'

.open-graph
  font-family: 'Gilroy-Light', sans-serif

  .open-graph__container
    max-width: 840px
    margin: 0 auto
    padding-top: 150px

  .open-graph__intrormation
    display: flex
    flex-direction: column
    align-items: center
    margin-bottom: 100px

.open-graph__title
  display: inline-block
  padding-bottom: 20px

.open-graph__title-gradient
  background: linear-gradient(92.9deg, #FFC000 0.24%, #F06966 100%)
  -webkit-background-clip: text
  -webkit-text-fill-color: transparent

.open-graph__title
  font-size: 46px
  margin-top: 0

.open-graph__subtitle
  font-size: 18px
  text-align: center
  padding-bottom: 20px

.open-graph__more-information
  font-size: 14px
  text-decoration: underline 0.5px

.open-graph__actions
  display: flex
  gap: 0 30px
  justify-content: center
  margin-bottom: 42px


.open-graph__link
  position: relative
  display: inline-block

.open-graph__link::after
  content: ""
  position: absolute
  bottom: -10px
  left: 0
  width: 100%
  height: 2px
  background: linear-gradient(92.9deg, #FFC000 0.24%, #F06966 100%)
  opacity: 0
  transition: opacity 0.3s

.open-graph__link:hover::after
  opacity: 1

.open-graph__form
  width: 840px
  height: 160px
  background: linear-gradient(92.9deg, rgba(255, 192, 0, 0.2) 0.24%, rgba(240, 105, 102, 0.2) 100%), #FFECB2
  border-radius: 6px
  margin-bottom: 100px

.open-graph__input-wrapper
  position: relative
  padding: 50px 12px 50px 120px

.open-graph__input-field
  width: 600px
  height: 60px
  padding: 23px 0px 23px 23px
  color: #868686
  font-size: 14px
  border-radius: 4px
  border: 1px solid #ddd
  margin-bottom: 10px
  transition: border-color 0.3s

.open-graph__input-field:focus
  outline: none
  border-color: #C4C4C4

.open-graph__submit-button
  position: absolute
  right: 120px
  background: linear-gradient(92.9deg, #FFC000 0.24%, #F06966 100%), #C4C4C4
  width: 174px
  height: 60px
  color: #fff
  font-size: 16px
  border: none
  border-radius: 6px
  padding: 10px 20px
  cursor: pointer

.open-graph__result
  margin-bottom: 42px
.open-graph__result-title
  text-align: center
  padding-bottom: 30px

.open-graph__result-nav-list
  display: flex
  gap: 0 30px
  justify-content: center
  position: relative

.open-graph__result-nav-link
  position: relative

.open-graph__result-nav-link::after
  content: ""
  position: absolute
  bottom: -10px
  left: 0
  width: 100%
  height: 2px
  background: linear-gradient(92.9deg, #FFC000 0.24%, #F06966 100%)
  opacity: 0
  transition: opacity 0.3s

.open-graph__result-nav-link:hover::after
  opacity: 1

.open-graph__data
  margin: 0 auto
  padding: 50px 200px 155px 200px
  width: 1240px
  height: 574px
  background-color: #FBFBFB

.open-graph__data-content
  width: 840px
  height: 488px
  background: #FFFFFF
  border: 2px solid #E0E2E7
  border-radius: 4px
  overflow: hidden

.open-graph__data-item-wrapper
  padding: 0 24px 0 24px

.open-graph__data-item
  margin-bottom: 10px

.open-graph__data-value
  font-weight: 600
  font-size: 24px
  word-break: break-all

.open-graph__data-value-link
  color: #939393

.open-graph__data-image
  max-width: 840px
  max-height: 369px
  width:100%
</style>
