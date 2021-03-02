<template>
	<view>
		<ms-tabs :list="list" v-model="active" :itemColor="itemColor" :lineColor="lineColor" 
			:class="{'sticky':sticky,'hideLine':!showLine}" @input="tabClick"
		></ms-tabs>
		<scroll-view scroll-y="true" :scroll-into-view="scrollToId" :scroll-with-animation="true" :style="{height:'1130rpx'}" @scroll="scrollToId = ''">
			<view class="content_box">
				<view class="content_box_item" v-for="(item,index) in cate" :key="index" :id="'item_' + index">
					<view class="title">{{item.name}}</view>
					<view class="list">
						<grid col="5" :border="0">
							<grid-item v-for="(ite,idx) in item.child_cate" :key="idx" @click="itemClick(ite)" 
								:order="idx" :iconImg="ite.logo_path"  :text="ite.name">
							</grid-item>
						</grid>
					</view>
				</view>
			</view>
		</scroll-view>
	</view>
</template>

<script>
	import msTabs from '@/components/ms-tabs/ms-tabs.vue';
	import Grid from '@/components/grid/grid.vue'
	import GridItem from '@/components/grid-item/grid-item.vue'
	export default{
		props:{
			sticky:{//是否固定顶部tab
				type:Boolean,
				default:true
			},
			showLine:{//是否显示底部线条
				type:Boolean,
				default:false
			},
			list:Array,//tabs的数据
			itemColor:String,//tab选中的颜色
			lineColor:String,//tab选中下划线的颜色
			lineAnimated:Boolean,//是否展示下划线滑动效果
			cate:Array,//循环的商品项
		},
		data(){
			return{
					active:0,//当前选中项对应的下标值
					scrollToId:'',//滚动到指定id
			}
		},
		components:{
			msTabs,
			Grid,
			GridItem
		},
		methods:{
			tabClick(){
				this.scrollToId = "item_" + this.active;
			},
			itemClick({id}){
				this.$emit('clickItem',id)
			}
		}
	}
</script>

<style lang="scss" scoped>
	/deep/.tabBlock{padding: 0 40rpx;
		&.sticky{position: sticky;top: 0rpx;z-index: 9;}
		&.hideLine .tab__line{display: none;}
		::-webkit-scrollbar{ width: 0; height: 0; color: transparent; }
	}
	.content_box{
		&_item{ width: 100%; background-color: #fff;	padding:0rpx 40rpx 30rpx; margin-bottom: 20rpx;box-sizing: border-box;
			.title{ font-size: 28rpx; color: #343A37; text-indent: 10rpx; height: 40rpx; line-height: 40rpx; margin: 10rpx 0; border-left: 8rpx solid #AADCBC; }
			.list{ display: flex; flex-wrap: wrap; justify-content: space-between;
				/deep/.grid{
					.sub{
						.o-img{width: 80rpx;height: 80rpx;}
						.o-text{text-align: center;}
					}
				}
			}
		}
	}
</style>
