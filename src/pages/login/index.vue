<template>
<div v-if="!hasLogined" class="form-wrap">
	<div class="form-item">
		<div class="form-left">帐号：</div>
		<div class="form-right">
			<input type="text" name="account" v-model="account" placeholder="请输入帐号" />
		</div>
	</div>
	<div class="form-item">
		<div class="form-left">密码：</div>
		<div class="form-right">
			<input type="text" name="password" v-model="password" placeholder="请输入密码" />
		</div>
	</div>
	<div>
		<text>{{returnData}}</text>
	</div>

	<div class="btn"><text class="btn-text" @click="doLogin">登录</text></div>
</div>
<div v-else>
	<div>{{userName}}，您好。您已经登录！以下为您的考勤记录：</div>
	<div>{{recordList}}</div>
	<div class="btn"><text class="btn-text" @click="doLogout">退出登录</text></div>
</div>
</template>

<script>
export default {
	data () {
		return {
			account: '',
			password: '',
			hasLogined: false,
			returnData: '',
			userName: '',
			recordList: null
		}
	},

	mounted () {
		let uid = wx.getStorage({
			key: 'userInfo', 
			success: res => {
				if (res.data != 'undefined' && res.data) {
					this.userName = JSON.parse(res.data).userName
					this.hasLogined = true
					this.getRecordList()
				}
			}
		})
	},

	methods: {
		doLogout () {
			wx.setStorage({
				key: 'userInfo', 
				data: 'undefined',
				success: () => {
					this.hasLogined = false
					this.userName = ''
				}
			})
		},

		doLogin () {
			let that = this
			let data = {
				account: '99901755',
				password: '123456'
			}
			wx.request({
				method: 'POST',
				//url: 'http://httpbin.org/post',
				url: 'http://www.smart-ecity.com/rest/services/irp/login',
				data: data,
				success: res => {
					let userName = res.data.realName
					let uid = res.data.smtId
					let jgbm = res.data.orgId
					this.setUserInfo({
						userName: userName,
						uid: uid,
						jgbm: jgbm
					})
				}
			})
		},

		getRecordList () {
			
		},

		setUserInfo (info) {
			wx.setStorage({
				key: 'userInfo', 
				data: JSON.stringify(info),
				success: () => {
					this.hasLogined = true
					this.userName = info.userName
				}
			})
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
	border-bottom-color: #cccccc;
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

.preview {
	width: 200px;
	height: 200px;
}
</style>
