<template>
	<div class="wrapper">
		<calculator/>
	</div>
</template>

<script>
import Calculator from '@/components/Calculator.vue'

export default {
  name: 'App',
  components: {
    Calculator
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.wrapper {
	display: flex;
	padding: 50px;
	justify-content: center;
	align-items: center;
	min-height: 100vh;
	background-color: #b1b5e5;
}
</style>
