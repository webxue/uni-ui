<template>
	<view class="">
		<view class="toolbar">
			<text v-for="(item,index) in toolbar" :key="index" @click="setStyle(item)" style="margin-right: 6px;">{{item.text}}</text>
		</view>
		<editor id="xEditor" placeholder="请输入内容..."></editor>
		<!-- 底部工具栏 -->
		<view class="bottom">
			<view class="list">
				
			</view>
			<view class="wrap">
				
			</view>
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				editor:null,
				// type 0 普通样式   1 分割线   2 插入图片 
				toolbar:[
					{name:'bold',text:'粗体',type:0},
					{name:'italic',text:'斜体',type:0},
					{name:'underline',text:'下划线',type:0},
					{name:'',text:'分割线',type:1},
					{name:'',text:'插入图片',type:2},
				]
			}
		},
		mounted() {
			uni.createSelectorQuery().select('#xEditor').context((res) => {
				this.editor = res.context
			}).exec()
		},
		methods:{
			setStyle({name,type}){
				if(type == 0){
					this.editor.format(name,name)
				}else if(type == 1){
					this.editor.insertDivider()
				}else if(type == 2){
					
				}
			}
		}
	}
</script>

<style lang="scss" scoped>
</style>
