<template>
	<view class="content">
		<button type="default" @click="$refs.xPayPwd._open()">打开支付弹窗</button>
		<x-pay-pwd ref="xPayPwd" :type="1" :maskClick="true" top="unset" :showClose="false" @change="change" :showHead="true" headText="请输入支付密码">
			<template #center>
				<button @click="clear">清空输入内容</button>
			</template>
		</x-pay-pwd>
	</view>
</template>

<script>
	export default {
		data() {
			return {
			}
		},
		methods: {
			// 监听输入框内容变化
			change({password}){
				console.log(password)
			},
			// 清空输入框内容,一般用于密码输错手动清空
			clear(){
				this.$refs.xPayPwd._clearKey();
			}
		}
	}
</script>

<style lang="scss" scoped>
</style>
