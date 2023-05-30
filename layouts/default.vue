<template>
	<div class="open-graph-header">
		<header class="open-graph-header__header">
			<div class="open-graph-header__logo">
				<img src="~/assets/svg/logotip-opengraph.svg" alt="Логотип" class="open-graph-header__logo-image" />
			</div>
			<div class="open-graph-header__login">
				<img src="~/assets/svg/door.svg" class="open-graph-header__login-icon" />
				<span class="open-graph-header__login-text">Войти в аккаунт</span>
			</div>
		</header>
	</div>
	<div>
		<slot />
	</div>
</template>

<style lang="sass" scoped>
@import url('https://fonts.cdnfonts.com/css/gilroy-bold')

.open-graph-header__header
  font-family: 'Gilroy-Light', sans-serif
  display: flex
  align-items: center
  justify-content: space-around
  padding: 10px
  background-color: #fff

.open-graph-header__logo
  margin-right: 10px

.open-graph-header__logo-image
  max-width: 100%

.open-graph-header__login
  display: flex
  align-items: center

.open-graph-header__login-icon
  fill: #000
  width: 24px
  height: 24px
  margin-right: 5px

.open-graph-header__login-text
  font-size: 16px
  cursor: pointer
</style>
