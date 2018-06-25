<template>
<div class="form-wrap">
	<div class="form-item">
		<div class="form-left">姓名：</div>
		<div class="form-right">
			<input type="text" name="name" v-model="name" placeholder="请输入您的姓名" />
		</div>
	</div>
	<div class="form-item">
		<div class="form-left">性别：</div>
		<div class="form-right">
			<picker :value="sexIndex" :range="sexList" @change="onChangeSex">
				<div class="picker">{{sexList[sexIndex]}}</div>
			</picker>
		</div>
	</div>
	<div class="form-item">
		<div class="form-left">头像：</div>
		<div class="form-right">
			<div class="image-picker" @click="onPickImage">
				<div v-if="imageData">
					<image class="preview" :src="imageData"></image>
				</div>
				<div v-else>请选择图片</div>
			</div>
		</div>
	</div>

	<div class="btn"><text class="btn-text">确认提交</text></div>
</div>
</template>

<script>
export default {
	data () {
		return {
			sexList: ['男', '女'],
			sexIndex: 0,
			name: '',
			imageData: ''
		}
	},

	methods: {
		onPickImage () {
			wx.chooseImage({
				count: 1,
				success: res => {
					let tempFilePath = res.tempFilePaths[0]
					this.imageData = tempFilePath
				}
			})
		},

		onChangeSex (e) {
			console.log(e);
			var index = +e.mp.detail.value;
			this.sexIndex = index;
		}
	}
}
</script>

<style scoped>
.form-item {
	box-sizing: border-box;
	margin-left: 25px;
	padding: 25px 25px 25px 0;
	border-bottom-width: 1px;
	border-bottom-style: solid;
	border-bottom-color: #ccc;
	display: flex;
	flex-direction: row;
}

.form-left {
	text-align: right;
	font-size: 28px;
	width: 100px;
}

.form-right {
	flex: 1;
	font-size: 28px;
}

.btn {
	width: 650px;
	padding: 25px 0;
	margin-left: 50px;
	background-color: #e8452f;
	margin-top: 60px;
}

.btn-text {
	width: 600px;
	display: block;
	text-align: center;
	font-size: 32px;
	color: #ffffff;
}
</style>
