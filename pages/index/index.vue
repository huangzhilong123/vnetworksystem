<template>
	<view class="container">
		
		<view class="title">管理系统</view>
		<text class="titlebelow">登录</text>
		<view class="account">账号</view>
		<view id="accountin">
			<input class="accountin" type="text" placeholder="请输入你的账号">
		</view>
		<view class="password">密码</view>
		<view id="passwordin">
			<input class="passwordin" @input="onInput" :type="showPassword?'text':'password'" :value="password" placeholder="请输入你的密码">
			<image 
			:src="showPassword?'/static/login/open.png':'/static/login/close.png'"
			class="pwd" @click="showPwd"></image>
		</view>
		<navigator url="../home/home" open-type="reLaunch"><button class="login">登录</button></navigator>
			
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				password:"",
				showPassword:true,
				inputType:"password"
			}
		},
		methods: {
			showPwd(e){
				this.showPassword = !this.showPassword;
			},
			onInput(e){
				this.password = e.target.value;
				console.log(this.password)
			}
		}
	}
</script>

<style>
	.container {
		padding: 20px;
		font-size: 14px;
		line-height: 24px;
		background: white;
		height: 580px;
	}
	.title{
		margin-left: 20px;
		margin-top: 30px;
		font-size: 18px;
	}
	.titlebelow{
		font-size: 24px;
		margin-left: 20px;
	}
	.account{
		opacity: 0.6;
		margin-left: 20px;
		margin-top: 40px;
	}
	#accountin{
		background: #EAEAEA;
		height: 40px;
		border-radius: 10px;
		line-height: 40px;
		margin-left: 20px;
		margin-top: 10px;
	}
	.accountin{
		margin-left: 20px;
		margin-top: 10px;
		position: absolute;
	}
	.password{
		opacity: 0.6;
		margin-left: 20px;
		margin-top: 40px;
	}
	#passwordin{
		background: #EAEAEA;
		height: 40px;
		border-radius: 10px;
		line-height: 40px;
		margin-left: 20px;
		margin-top: 10px;
	}
	.passwordin{
		margin-left: 20px;
		margin-top: 10px;
		position: absolute;
	}
	.login{
		background: #409EFF;
		width: 320px;
		margin-left: 20px;
		margin-top: 30px;
		border-radius: 10px;
	}
	.pwd{
		width: 20px;
		height: 20px;
		background-color: #EAEAEA;
		
		float: right;
		right:20px;
		top: 10px;
	}
</style>
