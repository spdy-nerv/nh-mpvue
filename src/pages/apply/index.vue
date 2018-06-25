<template>
	<div class="container">
		<text class="code-wrap">{{code}}</text>
		<form class="apply-form">
			<input type="text" name="code" v-model="code" placeholder="编码" />
		</form>
	</div>
</template>

<script>
export default {
	data() {
		return {
			code: '123456'
		}
	},

	mounted () {
		this.code = 'apply id: ' + this.$route.query.id;			
	},

	methods: {
	}
}
</script>

<style scoped>

</style>
