<template>
	<view class="content">
		<search-page placeholder="亲亲,输入内容哟~" :hotList="hotList" :hMax="5" :showHistory="true" :showHot="true" hType="round-fill" oType="square"></search-page>
	</view>
</template>

<script>
	import searchPage from '@/components/search-page/index.vue';
	export default {
		components:{
			searchPage
		},
		data() {
			return {
				hotList:['哇哈哈','喜之郎','优乐美','康师傅','尖叫']
			}
		}
	}
</script>

<style>
</style>
