<template>
	<div class="container">
		<text v-if="hasLogined">{{returnData}}</text>
		<div v-else>
			
		</div>
	</div>
</template>

<script>

export default {
	data () {
		returnData: null,
		hasLogined: true
	}
}
	
<script>
