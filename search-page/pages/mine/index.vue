<template>
	<view class="content">
		<view class="image">
			<image src="../../static/headImage.jpg" mode="aspectFit"></image>
		</view>
		<view class="list">
			<view class="item" v-for="(item,index) in infoList" :key="index" @click="handleClick(item)">
				<view class="name">{{item.name}}</view>
				<view class="text">{{item.text}}</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				infoList:[
					{name:'昵称',text:'xueshuai'},
					{name:'邮箱',text:'xueshuai_12@163.com'},
					{name:'网站',text:'http://xueshuai.top',online:'http://xueshuai.top'},
					{name:'QQ群',text:'1063233592',online:'https://qm.qq.com/cgi-bin/qm/qr?k=48lCCsUUYgxZh1eQGvJR9FDzqnwwyghJ&jump_from=webapi'},
					{name:'GitHub',text:'xue-shuai',online:'https://github.com/xue-shuai/uni-ui/scroll-view-page'},
					{name:'微信公众号',text:'叮当Ding',image:'https://img-blog.csdnimg.cn/20210202143040150.png'}
				]
			}
		},
		methods:{
			handleClick(item){
				let that = this;
				if(item.online){
					// #ifdef H5
					open(item.online)
					// #endif
					// #ifdef APP-PLUS
					plus.webview.open(item.online)
					// #endif
					// #ifndef H5 && APP-PLUS
					uni.showModal({
						title:'请打开浏览器访问'+item.online,
						confirmText:'复制链接',
						cancelText:'取消',
						success({confirm,cancel}) {
							if(confirm){
								that.copy(item.online)
							}
						}
					})
					// #endif
				}
				if(item.image){
					// #ifdef H5
					open(item.image)
					// #endif
					// #ifdef APP-PLUS
					uni.previewImage({
						urls:item.image
					})
					// #endif
					// #ifndef H5 && APP-PLUS
					uni.showModal({
						title:'请打开浏览器访问'+item.image,
						confirmText:'复制链接',
						cancelText:'取消',
						success({confirm,cancel}) {
							if(confirm){
								that.copy(item.image)
							}
						}
					})
					// #endif
				}
			},
			copy(data){
				// #ifndef H5
				uni.setClipboardData({
				    data:data,
				    success: function () {
							uni.showToast({ title:'复制成功', icon:'success' })
				    },
						fail: function(){
							uni.showToast({ title:'复制失败', icon:'none' })
						}
				});
				// #endif
				// #ifdef H5
				let input = document.createElement('input');
				input.setAttribute('readonly', 'readonly'); // 防止手机上弹出软键盘
				input.setAttribute('value', data);
				document.body.appendChild(input);
				input.select();
				let res = document.execCommand('copy');
				document.body.removeChild(input);
				uni.showToast({ title:'复制成功', icon:'success' })
				// #endif
			}
		}
	}
</script>

<style lang="scss" scoped>
	.content{display: flex;flex-direction: column;align-items: center;padding-top: 60rpx;
		.image{width: 200rpx;height: 200rpx;border-radius: 40rpx;overflow: hidden;margin-bottom: 40rpx;
			image{width: 100%;height: 100%;}
		}
		.list{box-sizing: border-box;padding: 0 40rpx;width: 100%;
			.item{width: 100%;display: flex;justify-content: space-between;padding: 30rpx 0;border-bottom: 2rpx solid #eee;
				&:last-of-type{border-bottom: none;}
				.name{color: #1f1f1f;font-size: 30rpx;}
				.text{color: #404040;font-size: 28rpx;}
			}
		}
	}
</style>
