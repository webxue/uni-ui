<template>
	<view style="width:100%;">
		<view v-if="title" class="o-title">{{title}}</view>
		<view class="grid"><slot /></view>
	</view>
</template>

<script>
	export default {
		name:'grid',
		props:{
			col:{
				type:[Number,String],
				default:3
			},
			border:{
				type:[Number,String],
				default:'true'
			},
			hoverClass:{
				type:String,
				default:''
			},
			title:{
				type:String,
				default:''
			}
		},
		
		provide() {
			return {
				col:this.col,
				border:this.border
			}
		},
		
		computed:{
			Col(){
				if (this.col < 2) return 2;
				else if(this.col > 5) return 5;
				else return this.col;
			}
		}
	}
</script>

<style lang="scss">

	.o-title{
		font-size:28rpx;
		color:#888;
		background-color:#f6f6f6;
		height:50rpx;
		line-height:50rpx;
		position:relative;
		padding-left:30rpx;
		padding-top:10rpx;
		box-sizing:content-box;
		&::after{
			position:absolute;
			content:"";
			left:10rpx;top:22rpx;
			height:24rpx;width:6rpx;
			border-radius:30px;
			background-color:#999;
			z-index:2;
		}
	}
	.grid {		width: 100%;		/* #ifdef MP */		position: relative;		box-sizing: border-box;		overflow: hidden;		/* #endif */		/* #ifndef MP */		display: flex;
		flex-direction: row;
		flex-wrap: wrap;		align-items: center;		/* #endif */	}

</style>
